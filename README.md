# Gynaptic [![Build Status](https://travis-ci.org/wagenaartje/gynaptic.svg?branch=master)](https://travis-ci.org/wagenaartje/gynaptic)
Gynaptic is an architecture-free [neural network](https://en.wikipedia.org/wiki/Artificial_neural_network) library with implementations to create [genetic neural networks](https://en.wikipedia.org/wiki/Neuroevolution). It gives the user the ability to create train neurol networks with evolutionary algorithms with just a few lines of code. The library is constantly updated with new mutation, crossover and selection methods. Gynaptics' main neural network code comes from the library [Synaptic](https://github.com/cazala/synaptic) by [Juan Cazala](https://github.com/cazala). Gynaptic will stay up to date with Synaptic's improvements as much as possible.

<img src="https://assets-cdn.github.com/images/modules/site/home-ill-work.png?sn" width="340px" align="right"/>

What Gynaptic adds to [Synaptic](https://github.com/cazala/synaptic):
- an easy-to-use genetic algorithm function
- 6 mutation methods
- 4 crossover methods
- 1 selection method
- 2 generation methods
- to/fromJSON for layers and neurons
- 3 (extra) squashing functions
- various code improvements
- overall extra functionality

Examples
- [Solve an XOR](https://wagenaartje.github.io/gynaptic/examples/xor/)

# Usage
Head over to the [wiki](https://github.com/wagenaartje/gynaptic/wiki) for documentation.

For the browser, embedding this code makes life easier:
```javascript
Neuron = gynaptic.Neuron;
Evolution = gynaptic.Evolution;
Trainer = gynaptic.Trainer;
Methods = gynaptic.Methods;
Layer = gynaptic.Layer;
Network = gynaptic.Network;
Architect = gynaptic.Architect;
```

# Example
This is an example of the creation and loop of a genetic neural network. The goal of this genetic algorithm is too create a population that will output a value that is as high as possible (=`1`) when inputted `0`. Please note that this is just an example, and this problem is much easier to 'solve' by backpropagating.

```js
// Create the evolutionary algorithm
var GNN = new Evolution({
  size: 50,
  elitism: 5,
  mutationRate: 0.05,
  networkSize = [1,4,1],
  mutationMethod: [Methods.Mutate.MODIFY_RANDOM_BIAS, Methods.Mutate.MODIFY_RANDOM_WEIGHT],
  crossOverMethod: [Methods.Crossover.UNIFORM, Crossover.AVERAGE],
  selectionMethod: [Methods.Selection.FITNESS_PROPORTIONATE],
  fitnessFunction: function(network){
     return Math.round(network.activate([0]) * 200);
  }
});

// Loop the evolution process until a certain average score is reached
var notFinished = true;;
while(notFinished){
  GNN.evaluate();
  if(GNN.getAverage() > 190){
    notFinished = false;
  }

  GNN.select();
  GNN.crossOver();
  GNN.mutate();
  GNN.replace();
};
```

If you want to know how to set up one of these algorithms yourself, feel free to take a look at the wiki pages! If you want to implement a genetic neural network algorithm, but don't know how, feel free to contact me at wagenaartje@protonmail.com!

# Installation
Gynaptic files are hosted by rawgit, just copy this link into the `<head>` tag:
```html
<script src="https://cdn.rawgit.com/wagenaartje/gynaptic/55b6d0d1/dist/gynaptic.js"></script>
```

Installing with node is also possible:

`npm install gynaptic`

# Plans
- Create pool generation methods :white_check_mark:
- Add SHIFT mutation method, which replaces a random connection somewhere else in the network :white_check_mark:
- Add ADD/REMOVE mutation method, which adds or removes a random neuron in a network :white_check_mark:
- Export/Import layers, neurons, evolutions to/from JSON :white_check_mark:
- Convolutional neural network, not sure if it will work out with synaptic yet :clock5:
- Add MODIFY_SQUASH mutation method, which changes the squash of a neuron randomly :white_check_mark:
- Refine code (updating code and removing unnecessary/unused code) IN PROGRESS
- Create extra LOSS functions
- Use `connections()` in the mutate functions

If you have any suggestions, please post them at the 'Issues' button at the top of the page.
