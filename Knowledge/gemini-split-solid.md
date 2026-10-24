# Splitting the Gemini class into three

All three go in `com.sefujo.resume.extractor`, the same package as now. Delete the old `GeminiResumeContentParser` and replace it with these.

Each class now has one job:

| Class | Its one job |
|---|---|
| `GeminiClient` | Talk to Gemini: model name, the call, error wrapping |
| `GeminiResumeContentParser` | Turn raw CV text into `ResumeContent` |
| `GeminiResumeTailor` | Turn BASE sections plus a job description into tailored sections |

## 1. GeminiClient.java

```java
package com.sefujo.resume.extractor;

import com.google.genai.Client;
import com.google.genai.types.GenerateContentResponse;
import com.sefujo.common.exception.LlmUnavailableException;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class GeminiClient {

    private final Client client;
    private final String model;

    public GeminiClient(Client client,
                        @Value("${gemini.model:gemini-3.5-flash-lite}") String model) {
        this.client = client;
        this.model = model;
    }

    public String generate(String prompt) {
        try {
            GenerateContentResponse response = client.models.generateContent(model, prompt, null);
            return response.text();
        } catch (Exception e) {
            throw new LlmUnavailableException("Cannot communicate with LLMs", e);
        }
    }
}
```

The model name now comes from `application.properties` (`gemini.model=...`). If you don't set it, it falls back to `gemini-3.5-flash-lite`.

## 2. GeminiResumeContentParser.java

```java
package com.sefujo.resume.extractor;

import com.sefujo.resume.content.ResumeContent;
import org.springframework.core.io.ClassPathResource;
import org.springframework.stereotype.Component;
import tools.jackson.databind.json.JsonMapper;

import java.io.IOException;
import java.nio.charset.StandardCharsets;

@Component
public class GeminiResumeContentParser implements ResumeContentParser {

    private final GeminiClient geminiClient;
    private final JsonMapper mapper;
    private final String promptTemplate;

    public GeminiResumeContentParser(GeminiClient geminiClient, JsonMapper mapper) throws IOException {
        this.geminiClient = geminiClient;
        this.mapper = mapper;
        this.promptTemplate = new ClassPathResource("prompts/prompt.txt")
                .getContentAsString(StandardCharsets.UTF_8);
    }

    @Override
    public ResumeContent parse(String rawText) {
        String prompt = promptTemplate.replace("{{RESUME_TEXT}}", rawText);
        String json = geminiClient.generate(prompt);
        return mapper.readValue(json, ResumeContent.class);
    }
}
```

## 3. GeminiResumeTailor.java

```java
package com.sefujo.resume.extractor;

import com.sefujo.resume.content.TailorSection;
import org.springframework.core.io.ClassPathResource;
import org.springframework.stereotype.Component;
import tools.jackson.databind.json.JsonMapper;

import java.io.IOException;
import java.nio.charset.StandardCharsets;

@Component
public class GeminiResumeTailor implements ResumeTailor {

    private final GeminiClient geminiClient;
    private final JsonMapper mapper;
    private final String promptTemplate;

    public GeminiResumeTailor(GeminiClient geminiClient, JsonMapper mapper) throws IOException {
        this.geminiClient = geminiClient;
        this.mapper = mapper;
        this.promptTemplate = new ClassPathResource("prompts/resumeTailor.txt")
                .getContentAsString(StandardCharsets.UTF_8);
    }

    @Override
    public TailorSection tailorSections(String description, TailorSection sections) {
        String sectionsJson = mapper.writeValueAsString(sections);
        String prompt = promptTemplate
                .replace("{{JOB_DESCRIPTION}}", description)
                .replace("{{RESUME_JSON}}", sectionsJson);
        String json = geminiClient.generate(prompt);
        return mapper.readValue(json, TailorSection.class);
    }
}
```

## 4. Changes in ResumeService

- Add `private final ResumeTailor resumeTailor;` and remove `private final JsonMapper jsonMapper;`.
- In `tailorResume`, delete the `writeValueAsString` line and call:

```java
TailorSection processedSection = resumeTailor.tailorSections(job.getDescription(), tailorSection);
```

## 5. Check it works

1. Run `./mvnw compile`.
2. Call the BASE endpoint for a fresh resume. It should still return 201 with parsed content.
3. Call the tailor endpoint for a new job. It should return 201, and 200 on the second call.

That proves both classes still work after the split.
