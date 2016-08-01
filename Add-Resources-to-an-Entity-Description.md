You can attach arbitrary data, called resources, to an entity. Resources can be used to document information about an entity, such as its collecting area or spectrum. Resources can be explicitly defined in an `EntityDescription`.

This tutorial shows how to add resources to an `EntityDescription`.

- [Step 1: Open or create an entity description](#step-1-open-or-create-an-entity-description)
- [Step 2: Add resources](#step-2-add-resources)

### Step 1: Open or create an entity description
Open or recreate the ["Demo" source description](Write-an-Entity-Description) so you have something to work with.

```matlab
classdef Demo < symphonyui.core.persistent.descriptions.SourceDescription

    methods

        function obj = Demo()
            obj.addProperty('id', '');
            obj.addProperty('sex', '');
        end

    end

end
```

### Step 2: Add resources
Add a resource named "spectrum" with data from a table by adding a line calling the `addResource()` method.

```matlab
table = [ ...
    321, 0.00;
    513, 0.72;
    741, 0.00];
obj.addResource('spectrum', table);
```

Add a resource named "collectingArea" with a value of 0.20 by adding another line calling the `addResource()` method.

```matlab
obj.addResource('collectingArea', 0.20);
```

The "Demo" description now defines two resources.

```matlab
classdef Demo < symphonyui.core.persistent.descriptions.SourceDescription

    methods

        function obj = Demo()
            obj.addProperty('id', '');
            obj.addProperty('sex', '');

            table = [ ...
                321, 0.00;
                513, 0.72;
                741, 0.00];
            obj.addResource('spectrum', table);
            obj.addResource('collectingArea', 0.20);
        end

    end

end
```

Resources can be accessed within protocols by using the `getResource()` method.

```matlab
experiment = obj.persistor.experiment;
sources = experiment.sources;
demoSource = sources{1};
spectrum = demoSource.getResource('spectrum');
collectingArea = demoSource.getResource('collectingArea');
```
