Tensorflow.js is a library that enables you to run machine learning algorithms on the browser. But there is a problem
using it - the training of th model takes a lot of time. To solve this people make and train the model they want in python
and they save the weights in a file which they use to load the **pretrained** model on the browser to reduce the time taken normally to 
train the model. Here you will learn to do just that.

First you have to create the model in python. I did it using the keras API of tensorflow. Once you've created the model you have to compile it
it - using ```model.compile()``` - and train it - using ```model.fit()```. Once you've done that you must save the model using the
code - ```model.save_weights("filename.h5")```.

Now that you have the file with all the weights you should move it to the folder where you will be making the web page to make the process of
converting the file to a ```.json``` format (its more web-friendly) more easily. To convert it to a ```.json``` format you must open you command
line interface in your computer and type in ```cd [the directory where your file is kept]```. After you've done that type in ```python pip
install virtualenv```(do this only if you haven't installed virtualenv on your computer before). Once virtualenv is installed, type in
```virtualenv --no-site-packages env``` and after that type in ```env\Scripts\activate.bat``` to activate your virtual environment.

Now that you've done that, on your virtualenv type in ```pip install tensorflowjs```. Once it is installed type in
```tensorflowjs_converter \--input_format=keras \filename.h5 \ [directory you want your json model to go to]```. This outputs a 
```model.json``` to a directory of your choice.

After you're done with all of this you must include the code - ```const layersModel = await tf.loadGraphModel(‘[path]/model.json’);``` 
in your javascript file. This creates a layers model for you in tensorflow.js. If you want a graph model you include the code - 
```const graphModel = await tf.loadLayersModel(‘path/to/model.json’);``` in your javascript file.

Now we're done with all of the loading of the pretrained models. But you must still be wondering what the difference is between 
a [graph model](https://js.tensorflow.org/api/latest/#class:GraphModel) and a [layers model](https://js.tensorflow.org/api/latest/#class:LayersModel). A layers model is built using the [tf layers API](https://js.tensorflow.org/api/latest/#Layers) 
in tensorflow.js and has more methods for predicting and evaluating than a graph model. A graph model on the other hand has less methods than a 
layers model for prediction and evaluation of a model and is something I would not use. I would use a layers model because it has more
methods than a graph model (even options for 
training).
