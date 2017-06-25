# Easygen

EasyGen is a visual user interface to help set up simple neural network generation tasks.

There are a number of neural network frameworks (Tensorflow, TFLearn, Keras, PyTorch, etc.) that implement standard algorithms for generating text (e.g., recurrent neural networks, sequence2sequence) and images (e.g., generative adversarial networks). They require some familairity with coding. Beyond that, just running a simple experiment may require a complex set of steps to clean and prepare the data.

For example: to use a neural network to generate a history for a fictional country, I would:
1. Get superhero names from somewhere. If it is Wikipedia, we see a lot of names are followed by parentheticals.
2. Strip off parenthetical information.
3. Remove empty lines and strip off any whitespace at the end of lines.
4. Feed the resultant file into a character-rnn algorithm.
5. Run the resultant model and store the outputs to a file.

EasyGen allows one to quickly set up the data cleaning and neural network training pipeline using a graphical user interface and a number of self-contained "modules" that implement stardard data preparation routines. EasyGen differs from other neural network user interfaces in that it doesn't focus on the graphical instantiation of the neural network itself. Instead, it provides an easy to use way to instantiate some of the most common neural network algorithms used for generation. EasyGen focuses on the data preparation.

Here is how EasyGen can be used to run the superhero name generation example above:
![alt text](https://raw.githubusercontent.com/markriedl/easygen/master/web/lstm.png "Screenshot of EasyGen setup to run an LSTM")
Each box is a chunk of standard code that can be selected from a library of options. Arrows indicate the data flow from module to module.
 
## Preliminaries

What is a neural network? A neural network is a machine learning algorithm very loosely inspired by the brain. I'm not a fan of the brain metaphor (see [introduction to neural networks without the brain metaphor](https://medium.com/@mark_riedl/introduction-to-neural-nets-without-the-brain-metaphor-874e7950bca0)).

What you need to know is that a neural network is an automated function approximation technique. If you remember back to grade school, your teacher might have asked you to solve a problem like this:

![](https://raw.githubusercontent.com/markriedl/easygen/master/web/function.png =100x)

That is, given the inputs and outputs, guess the function that turns the inputs into outputs. Probably you could figure out the exact function (`y = 2x + 1`). How did you do it? You might have guessed a function based on the first example, like `y = x + 2` and then checked to see if it worked on the next example. This guess won't work: `x=2` gives `y=4`, which is off by 1. So you probably updated your guess to `y = 2x + 1`. Now that example is right. What about the next example? Yup. What about the previous example? Yup.

That is more or less the process that a neural network goes through to approximate a function. Except it doesn't just work on algebra equations. It turns out that one can set up a graph of nodes and edges that connect inputs to outputs and allow information to flow through the box. If the weights on the edges are designed correctly, then the box will generate the right answer for any given input. 

![alt text](https://raw.githubusercontent.com/markriedl/easygen/master/web/neural-net.png "A conceptual diagram of a neural network")

Neural network training is a process of constructing a lot of examples of inputs and outputs and running them through the network graph. When the the network gives the wrong answer, some of the weights are fiddled with so that the answer is closer to the desired output. Then you run the examples through the network again (each time you do this is called an *epoch*) to make sure the weight fiddling didn't screw anything up. Do this enough times and the weights will converge on some numbers that make the network produce the right answer (or close to the right answer) more often than not.

Now that the network has been trained--that is, we have a really good guess about the function that might have generated the data--we can apply run the neural network on inputs we have never seen before and have some confidence that it does the right thing.
