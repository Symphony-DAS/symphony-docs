# Add Resources to a Device

You can attach arbitrary data, called resources, to a device. Resources can be used to document information about a device, such as its calibration data or spectrum. Resources can be explicitly defined in a `RigDescription`.

This tutorial shows how to add resources to a device within a `RigDescription`.

- [Step 1: Open or create a rig description](#step-1-open-or-create-a-rig-description)
- [Step 2: Add resources](#step-2-add-resources)

### Step 1: Open or create a rig description
Open or recreate the ["Demo" description](Write-a-Rig-Description.md) so you have something to work with.

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

### Step 2: Add resources
Add a resource named "spectrum" with data from a table to the "Green LED" device by adding a line calling the `addResource()` method.

```matlab
table = [ ...
    321, 0.00;
    513, 0.72;
    741, 0.00];
green.addResource('spectrum', table);
```

Add a resource named "calibration" with a value of 1.2 to the "Green LED" device by adding another line calling the `addResource()` method.

```matlab
green.addResource('calibration', 1.2);
```

The "Green LED" device now has two resources.

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
            table = [ ...
                321, 0.00;
                513, 0.72;
                741, 0.00];
            green.addResource('spectrum', table);
            green.addResource('calibration', 1.2);
            obj.addDevice(green);
        end

    end

end
```

Resources can be accessed within protocols by using the `getResource()` method.

```matlab
green = obj.rig.getDevice('Green LED');
table = green.getResource('spectrum');
value = green.getResource('calibration');
```
