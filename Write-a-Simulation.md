# Write a Simulation

This tutorial shows you how to write a `Simulation`.

- [Step 1: Create a function](#step-1-create-a-function)
- [Step 2: Loop through active input streams](#step-2-loop-through-active-input-streams)

### Step 1: Create a function
A `Simulation` is simply a MATLAB function with a particular set of inputs and outputs.

Create a new function in your Symphony [package](Create-a-Package.md) by navigating to the package in MATLAB's **Current Folder**, right-clicking on the "+simulations" directory, and selecting **New File > Function**.

![new function](images/write-a-simulation/new-function.png)

Name the function file "demo.m" and open it in the MATLAB Editor.

```matlab
function [ output_args ] = demo( input_args )
%DEMO Summary of this function goes here
%   Detailed explanation goes here


end
```

Remove the comments and edit the function line to accept three inputs named "daq", "outputMap", and "timeStep" and return one output named "inputMap".

```matlab
function inputMap = demo(daq, outputMap, timeStep)

end
```

You now have an empty `Simulation`.

### Step 2: Loop through active input streams
