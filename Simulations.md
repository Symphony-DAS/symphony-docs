---
description: Create simulations to test protocols and models
---

# Simulations
A `Simulation` is an algorithm that simulates data acquired by data acquisition hardware. The purpose of simulations is twofold:

1. Allows testing protocol and stimulus generation code independent of hardware.
2. Allows the use of Symphony for computational simulation in addition to direct data acquisition. In this mode, the same application shell, protocol and stimulus generation code can be used for both physiology and simulation experiments, with the resulting output in the common Symphony data format.

## Tutorials
<ul class="list-unstyled">
<li><a href="Write-a-Simulation.md">Write a Simulation</a></li>
<li><a href="Set-the-Simulation-for-a-DAQ-Controller.md">Set the Simulation for a DAQ Controller</a></li>
</ul>

## Examples
<ul class="list-unstyled">
<li><a href="https://github.com/Symphony-DAS/symphony-matlab/blob/master/src/main/matlab/%2Bsymphonyui/%2Bbuiltin/%2Bsimulations/Loopback.m">Loopback</a></li>
</ul>
