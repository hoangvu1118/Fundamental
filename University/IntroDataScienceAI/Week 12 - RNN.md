RNN - It is good at processing sequence data for predictions
![[Pasted image 20250520021206.png | 400]]
The input at timestep at 1 
After going through a sequence of timestep --> go through multiple weighted connection
--> it is either go to zero or explode --> therefor going to timestep `n` is somewhat impossible 
**that is the problem of RNN**
![[Pasted image 20250520021316.png | 350]]

## LSTM - Network architecture
Long short term memory
+ Hidden layer unit is now an LSTM cell unit
+ LSTM cells can *remember* the states of hidden layers through time

![[Pasted image 20250520021751.png | 400]]
The below is LSTM
LSTM has cell state and hidden state
--> Cell state has no *weighted sum* -> so it is fed with no W
which makes it no loss information

The cell state (channel) is maintained so the program can remember the input from state to state

## LSTM Cells 
+ 3 data flows (input, output, memory) are control by 3 gates
![[Pasted image 20250520022849.png | 250]]![[Pasted image 20250520023145.png]]

```
- Gate unit
- Can control data flow pass through it
- Implementation:
	- DataOut = DataIn * ControlSignal
	- ControlSignal  = 1 🡪 Data can pass through
	- ControlSignal = 0 🡪 Data can not pass through
```
![[Pasted image 20250520023333.png | 300]]

First sigmoid function  
Since sigmoid range from 0 to 1
--> implement a *Gate output* --> So the first sigmoid function will be a
**FORGET GATE** to decide whether we want the information from the previous state or not

Second gate - Second sigmoid function --> input gate
Control the information from previous state and the *input flow*
To update the information to the *cell channel*

The third gate - the third sigmoid function --> output gate
the path from cell channel --> output through `tanh --> x` 
Is the output information --> then the output gate will control
If it is 0 then both of the output will be zero otherwise 1
--> However the cell channel would be affected

