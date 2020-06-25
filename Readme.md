FPGA-SoC-Linux-Example-1-ZYBO-Z7
================================

FPGA-SoC-Linux example(1) binary and project and test code for ZYBO-Z7

### Requirement

* Board: ZYBO-Z7
* OS: [FPGA-SoC-Linux](https://github.com/ikwzm/FPGA-SoC-Linux.git)

## Install

### Install python3-numpy

```
shell# apt-get install python3-numpy
```

### Download FPGA-SoC-Linux-Example-1-ZYBO-Z7

```
shell$ git clone https://github.com/ikwzm/FPGA-SoC-Linux-Example-1-ZYBO-Z7
shell$ cd FPGA-SoC-Linux-Example-1-ZYBO-Z7
```

### Install to FPGA and Device Tree

```
shell# rake install
dtbocfg.rb --install uio_irq_sample --dts uio_irq_sample.dts
<stdin>:22.13-27.20: Warning (unit_address_vs_reg): /fragment@1/__overlay__/pump-uio: node has a reg or ranges property, but no unit name
<stdin>:9.13-41.4: Warning (avoid_unnecessary_addr_size): /fragment@1: unnecessary #address-cells/#size-cells without "ranges" or child "reg" property
[ 1150.975458] fpga_manager fpga0: writing pump_axi4.bin to Xilinx Zynq FPGA Manager
[ 1151.049447] OF: overlay: WARNING: memory leak will occur if overlay removed, property: /amba/fpga-region0/firmware-name
[ 1151.062245] fclkcfg amba:fclk0: driver installed.
[ 1151.066958] fclkcfg amba:fclk0: device name    : fclk0
[ 1151.072799] fclkcfg amba:fclk0: clock  name    : fclk0
[ 1151.077939] fclkcfg amba:fclk0: clock  rate    : 99999999
[ 1151.083443] fclkcfg amba:fclk0: clock  enabled : 1
[ 1151.097854] u-dma-buf udmabuf4: driver version = 3.0.1
[ 1151.103131] u-dma-buf udmabuf4: major number   = 243
[ 1151.108091] u-dma-buf udmabuf4: minor number   = 0
[ 1151.113414] u-dma-buf udmabuf4: phys address   = 0x30100000
[ 1151.118985] u-dma-buf udmabuf4: buffer size    = 1048576
[ 1151.124355] u-dma-buf udmabuf4: dma device     = amba:pump-udmabuf4
[ 1151.130624] u-dma-buf udmabuf4: dma coherent   = 0
[ 1151.135462] u-dma-buf amba:pump-udmabuf4: driver installed.
[ 1151.146995] u-dma-buf udmabuf5: driver version = 3.0.1
[ 1151.152216] u-dma-buf udmabuf5: major number   = 243
[ 1151.157177] u-dma-buf udmabuf5: minor number   = 1
[ 1151.162063] u-dma-buf udmabuf5: phys address   = 0x30200000
[ 1151.167636] u-dma-buf udmabuf5: buffer size    = 1048576
[ 1151.172999] u-dma-buf udmabuf5: dma device     = amba:pump-udmabuf5
[ 1151.179267] u-dma-buf udmabuf5: dma coherent   = 0
[ 1151.184108] u-dma-buf amba:pump-udmabuf5: driver installed.
```

## Run sample1 or sample2

### Compile sample1 or sample2

```
shell# rake sample1 sample2
```

### Run sample1

```
shell# ./sample1
time = 0.005896 sec
time = 0.005954 sec
time = 0.005917 sec
time = 0.005864 sec
time = 0.005963 sec
time = 0.005935 sec
time = 0.005925 sec
time = 0.005893 sec
time = 0.005916 sec
time = 0.005903 sec
```

### Run sample2

```
shell# ./sample2
time = 0.005907 sec
time = 0.005948 sec
time = 0.005917 sec
time = 0.005929 sec
time = 0.005916 sec
time = 0.005960 sec
time = 0.005904 sec
time = 0.005975 sec
time = 0.005909 sec
time = 0.005946 sec
```

## Run sample.py

```
shell# python3 sample.py
elapsed_time:5.948[msec]
elapsed_time:5.874[msec]
elapsed_time:5.882[msec]
elapsed_time:5.888[msec]
elapsed_time:5.865[msec]
elapsed_time:5.876[msec]
elapsed_time:5.86[msec]
elapsed_time:5.882[msec]
elapsed_time:5.889[msec]
average_time:5.885[msec]
thougput    :178.178[MByte/sec]
udmabuf4 == udmabuf5 : OK
```

## Uninstall

```
shell# rake uninstall
dtbocfg.rb --remove uio_irq_sample
[ 1581.796569] u-dma-buf amba:pump-udmabuf5: driver removed.
[ 1581.803265] u-dma-buf amba:pump-udmabuf4: driver removed.
[ 1581.812765] fclkcfg amba:fclk0: driver unloaded
```


## Build Bitstream file

### Requirement

* Vivado 2016.1 - 2017.2.1

### Download FPGA-SoC-Linux-Example-1-Base

```
shell$ pushd FPGA-SoC-Linux-Example-1-Base
shell$ git submodule init
shell$ git submodule update
shell$ popd
```

### Create Project

```
Vivado > Tools > Run Tcl Script > project/create_project.tcl
```

### Implementation

```
Vivado > Tools > Run Tcl Script > project/implementation.tcl
```

### Convert from Bitstream File to Binary File

```
shell$ tools/fpga-bit-to-bin.py --flip project/project.run/impl_1/design_1_wrapper.bit pump_axi4.bin
```
