# PUMA Simulator

Below you will find some information on how to use the PUMA Simulator.

## Table of Contents

- [Introduction](#introduction)
- [System requirements](#system-requirements)
- [Quick Start](#quick-start)
- [Usage](#usage)
- [Citation](#citation)
- [Authors](#authors)

## Introduction
This emulator was created as a result of the work described in the PUMA paper (https://dl.acm.org/citation.cfm?id=3304049). Details of the hardware architectture and compiler can be found there. 

## System requirements

Below you can find the system requirements and versions tested.

| Requirement | Version                    |
| ----------- | -------------------------- |
| OS: Ubuntu  | 16.04.3 LTS (Xenial Xerus) |
| Python      | 2.7.12                     |

## Quick Start

```sh
sudo apt-get install python-tk

sudo pip install http://download.pytorch.org/whl/cu80/torch-0.3.0.post4-cp27-cp27mu-linux_x86_64.whl

sudo pip install -r <dpe_emulate>/requirements.txt

```

If you are behind a proxy, you should type ```
sudo pip --proxy $http_proxy install ...``` instead.

## Usage

### Emulate
For testing if everything is working fine:

```sh
cd <dpe_emulate>/src

python dpe.py
```

Then, you should see some results like:

```sh
...

('Cycle: ', 8783, 'Tile halt list', [1, 1, 0, 1])
('Cycle: ', 8784, 'Tile halt list', [1, 1, 0, 1])
('Cycle: ', 8785, 'Tile halt list', [1, 1, 0, 1])
('Cycle: ', 8786, 'Tile halt list', [1, 1, 1, 1])
cycle: 8786 Node Halted
Finally node halted | PS: max_cycles 10000
('Dumping tile num: ', 0)
('Dumping tile num: ', 1)
('Dumping tile num: ', 2)
('Dumping tile num: ', 3)
Output Tile dump finished
Success: Hadrware results compiled!!
```
### Running a compiled model
This emulator executes models compiled by PUMA Compiler (https://github.com/illinois-impact/puma-compiler). 

After you compile a model using the compiler, in order to execute it with the DPE emulator, follow the steps below?
1- Copy <dpe_emulate>/test/generate-py.sh file to the <dpe_compiler>/test folder (you only need to do this once).
2- Edit <dpe_emulate>/test/generate-py.sh file, line 4 and change the value of SIMULATOR_PATH variable.
```sh

SIMULATOR_PATH="<emulator_root_path>"

```
3- Execute the generate-py.sh script
4- Look at the number of tiles generated by the compiler for ths model and update the value of "num_tile_compute" entry in <dpe_emulator_root>/include/config.py file to match the number fo compute tiles generated by compiler (remember that Til0 and Tile1 are used for input and output)
5- Go to emulator src directory (<emulator_root>/src) and execute dpe.py:
```sh
python2 dpe.py -n <model_name>
```

## Citation
Please cite the following paper if you find this work useful:

* A. Ankit, I. El Hajj, S. Chalamalasetti, G. Ndu, M. Foltin, R. S. Williams, P. Faraboschi, W.-M. Hwu, J. P. Strachan, K. Roy, D. Milojicic. **PUMA: A Programmable Ultra-efficient Memristor-based Accelerator for Machine Learning Inference**. In Proceedings of the Twenty-Fourth International Conference on Architectural Support for Programming Languages and Operating Systems (ASPLOS), 2019.

## Authors

Aayush Ankit, Plinio Silveira, Glaucimar Aguiar
