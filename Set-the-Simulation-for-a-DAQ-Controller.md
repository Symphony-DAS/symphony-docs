# Set the Simulation for a DAQ Controller

A `Simulation` may be set on any `SimulationDaqController` subclass. Symphony comes with two built-in `SimulationDaqController` subclasses:

- `symphonyui.builtin.daqs.HekaSimulationDaqController` - Manages a simulated HEKA (InstruTECH) DAQ interface (requires no attached hardware).
- `symphonyui.builtin.daqs.NiSimulationDaqController` - Manages a simulated National Instruments DAQ interface (requires no attached hardware).

This tutorial shows how to set the simulation for a `SimulationDaqController`.

- [Step 1: Open or create a rig description](#step-1-open-or-create-a-rig-description)
- [Step 2: Set the simulation for the controller](#step-2-set-the-simulation-for-the-controller)

### Step 1: Open or create a rig description
Open or recreate the ["Demo" rig description](Write-a-Rig-Description.md) so you have something to work with.

```matlab
classdef Demo < symphonyui.core.descriptions.RigDescription

    methods

        function obj = Demo()
            import symphonyui.builtin.daqs.*;
            import symphonyui.builtin.devices.*;

            daq = HekaSimulationDaqController();
            obj.daqController = daq;

            % Add a MultiClamp 700B device with name = Amp, channel = 1
            amp = MultiClampDevice('Amp', 1).bindStream(daq.getStream('ao0')).bindStream(daq.getStream('ai0'));
            obj.addDevice(amp);

            % Add a LED device with name = Green LED, units = volts
            green = UnitConvertingDevice('Green LED', 'V').bindStream(daq.getStream('ao1'));
            obj.addDevice(green);
        end

    end

end
```

### Step 2: Set the simulation for the controller
You set the simulation for a simulation controller by setting its "simulationRunner" property to a [function handle](https://www.mathworks.com/help/matlab/matlab_prog/creating-a-function-handle.html) of a simulation function.

Add an additional line after instantiating the simulation controller (i.e. `daq = HekaSimulationDaqController`) and set its "simulationRunner" property to a function handle of the ["demo" simulation function](Write-a-Simulation.md).

```matlab
classdef Demo < symphonyui.core.descriptions.RigDescription

    methods

        function obj = Demo()
            import symphonyui.builtin.daqs.*;
            import symphonyui.builtin.devices.*;

            daq = HekaSimulationDaqController();
            daq.simulationRunner = @edu.washington.riekelab.simulations.demo;
            obj.daqController = daq;

            ...
        end

    end

end
```

<table cellspacing="0" class="note" summary="Note" cellpadding="5" border="1"><tbody><tr width="90%"><td>
<b>Note:</b> For this to work, you must have completed the "Write a Simulation" tutorial so that the "demo" simulation exists and replace the `edu.washington.riekelab` prefix with your own package prefix.
</td></tr></tbody></table>
