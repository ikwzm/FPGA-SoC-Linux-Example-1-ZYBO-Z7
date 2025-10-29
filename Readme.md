FPGA-SoC-Linux-Example-1-ZYBO-Z7
================================

FPGA-SoC-Linux example(1) binary and project and test code for ZYBO-Z7

### Requirement

* Board: ZYBO-Z7
* OS:
   + ~~[FPGA-SoC-Linux](https://github.com/ikwzm/FPGA-SoC-Linux.git)~~
   + [FPGA-SoC-Debian12](https://github.com/ikwzm/FPGA-SoC-Debian12.git)
   + [FPGA-SoC-Debian13](https://github.com/ikwzm/FPGA-SoC-Debian13.git)

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
<stdin>:22.13-27.20: Warning (unit_address_vs_reg): /fragment@1/[ 2561.587342] fpga_manager fpga0: writing pump_axi4.bin to Xilinx Zynq FPGA Manager
__overlay__/pump-uio: node has a reg or ranges property, but no unit name
<stdin>:9.13-41.4: Warning (avoid_unnecessary_addr_size): /fragment@1: unnecessary #address-cells/#size-cells without "ranges", "dma-ranges" or child "reg" property
[ 2561.965598] OF: overlay: WARNING: memory leak will occur if overlay removed, property: /axi/fpga-region0/firmware-name
[ 2561.980963] fclkcfg axi:fclk0: driver version : 1.9.0
[ 2561.986042] fclkcfg axi:fclk0: device name    : axi:fclk0
[ 2561.995829] fclkcfg axi:fclk0: clock  name    : fclk0
[ 2562.003056] fclkcfg axi:fclk0: clock  rate    : 99999999
[ 2562.008401] fclkcfg axi:fclk0: clock  enabled : 1
[ 2562.019284] fclkcfg axi:fclk0: driver installed.
[ 2562.061704] u-dma-buf udmabuf4: driver version = 5.3.0
[ 2562.066898] u-dma-buf udmabuf4: major number   = 243
[ 2562.075407] u-dma-buf udmabuf4: minor number   = 0
[ 2562.080218] u-dma-buf udmabuf4: phys address   = 0x3c100000
[ 2562.086001] u-dma-buf udmabuf4: buffer size    = 1048576
[ 2562.091389] u-dma-buf axi:pump-udmabuf4: driver installed.
[ 2562.104893] u-dma-buf udmabuf5: driver version = 5.3.0
[ 2562.110064] u-dma-buf udmabuf5: major number   = 243
[ 2562.115119] u-dma-buf udmabuf5: minor number   = 1
[ 2562.119931] u-dma-buf udmabuf5: phys address   = 0x3c200000
[ 2562.125562] u-dma-buf udmabuf5: buffer size    = 1048576
[ 2562.130917] u-dma-buf axi:pump-udmabuf5: driver installed.
```

## Run sample1 or sample2

### Compile sample1 or sample2

```
shell# rake sample1 sample2
```

### Run sample1

```
shell# ./sample1
elapsed_time = 5.930491 [msec]
elapsed_time = 5.933923 [msec]
elapsed_time = 5.924665 [msec]
elapsed_time = 5.906281 [msec]
elapsed_time = 5.932825 [msec]
elapsed_time = 5.918437 [msec]
elapsed_time = 5.931835 [msec]
elapsed_time = 5.895889 [msec]
elapsed_time = 5.878537 [msec]
elapsed_time = 5.927797 [msec]
```

### Run sample2

```
shell# ./sample2
elapsed_time = 5.945107 [msec]
elapsed_time = 5.936888 [msec]
elapsed_time = 5.909672 [msec]
elapsed_time = 5.918029 [msec]
elapsed_time = 5.937379 [msec]
elapsed_time = 5.935616 [msec]
elapsed_time = 5.924377 [msec]
elapsed_time = 5.915359 [msec]
elapsed_time = 5.944891 [msec]
elapsed_time = 5.942011 [msec]
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
