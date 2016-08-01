# File Format

Symphony persists data in the [HDF5 file format](https://www.hdfgroup.org/HDF5/). The figure below shows the basic structure of a Symphony data file. Each entity is represented as an HDF5 group. Each file comprises a single experiment entity, which is the only top level group.

![overview](images/file-format/overview.png)

## Details

### File
![file](images/file-format/file.png)

### Experiment
![experiment](images/file-format/experiment.png)

### Device
![device](images/file-format/device.png)

### Source
![source](images/file-format/source.png)

### Epoch Group
![epoch group](images/file-format/epoch-group.png)

### Epoch Block
![epoch block](images/file-format/epoch-block.png)

### Epoch
![epoch](images/file-format/epoch.png)

### Background
![background](images/file-format/background.png)

### Response
![background](images/file-format/response.png)

### Stimulus
![background](images/file-format/stimulus.png)

### Resource
![resource](images/file-format/resource.png)
