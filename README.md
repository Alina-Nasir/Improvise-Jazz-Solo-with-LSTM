## LSTM on Jazz Solo Dataset
### Project Overview
The model used in this project is of one to many LSTM architecture. The model is trained on random snippets of 30 values taken from longer piece of music.
### Building LSTM Model
The following steps were taken to build the model
#### 1. Sequence generation using a for-loop
If the input sequence is known in advance then RNN architecture can be built using simple Keras model. But in case of sequence generation you cannot know all values of xt in advance. Hence xt is generated one at a time using yt-1. The input at time “t” is the prediction at the previous step “t-1”. Therefore, a for loop has been implemented to iterate over the time steps.
#### 2. Shareable weights
In the implementation of the djmodel() function, it is crucial to iterate through the LSTM layer Tx times using a for-loop. Maintaining consistency in weights across all Tx instances is paramount for effective sharing of parameters. This necessitates the use of a globally defined shared layer, ensuring that the same layer-object instance is referenced throughout.
To achieve this, the following key steps should be taken:
  1. Define the layer objects, employing global variables for this purpose.
  2.	When forwarding the input, invoke these predefined layer objects to ensure that the shared weights are consistently utilized across all Tx steps. This not only promotes efficiency but also avoids the re-initialization of weights, fostering the desired shared parameterization in the Keras model.
#### 3. 3 types of layer:
  1.	Reshape(): Reshapes an output to certain shape
  2.	LSTM(): Long Short Term Memory Layer
  3.	Dense():  A regular fully-connected neural network layer.
#### 4. Model Training
After creating the model it is complied for training. For this purpose, Adam is used as optimizer and categorical cross-entropy is used as loss function.
#### 5. Generating Music
During each sampling step, the process involves the following:
  1.	Utilize the activation 'a' and cell state 'c' from the previous state of the LSTM as input.
  2.	Perform forward propagation for one step.
  3.	Obtain a new output activation and cell state.
     
Subsequently, the newly obtained activation 'a' is employed for generating the output through the fully connected layer, denoted as 'densor'.
In the initialization phase, the following variables are set to zero:
  1.	x0
  2.	Hidden state a0
  3.	Cell state c0

This ensures a consistent starting point for the LSTM model, setting the initial values for input, hidden state, and cell state to zeros before the sampling process begins.
