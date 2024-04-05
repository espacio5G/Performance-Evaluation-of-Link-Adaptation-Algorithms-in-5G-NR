# Performance Evaluation of Link Adaptation Algorithms in 5G NR

This repository contains the code used to simulate the different scenarios and algorithms mentioned in the paper of the same name. The code is divided into simulator scripts (cpp code), post-processing and auxiliary scripts (bash scripts), and plot scripts (python scripts).

## Description

The code in this repository runs a 5G Stand-Alone simulation using the ns-3 discrete event network simulator and 5G-LENA module. There are 2 important scenarios and 4 different algorithms, the scenarios are:

1. Indoor Router: which simulates 2 users that have a 5G router inside their apartments connected to a gNb in a lamp post on the curb. The users are in the 5th and 8th floors.
2. Trees: a moving user and a gNb are on opposite sides of a grove.

The link adaptation algorithms tested focus on changing the target BLER (maximum value permitted), with the intent to make better use of the physical channel.

The algorithms are as follows:

1. Fixed target BLER of 0.1
2. Fixed target BLER of 0.3
3. Dynamic BLER based on the paper [Optimizing the Target Error Rate for Link Adaptation](https://ieeexplore.ieee.org/abstract/document/7417770)
4. Hybrid Dynamic-Fixed BLER (a combination of algorithms 1 and 3)

All combinations of scenarios and algorithms are possible and the simulation outputs different metrics, such as SINR, retransmissions, lost packets, BLER values, CQI values, delay, etc.

_This is a snapshot of the code related to 5G-Research in FCFM, the repository with the latest changes and other works may be found at [this GitHub repo](https://github.com/SirCrocker/5G-Research-FCFM)_

## Getting Started

### Dependencies

* ns-3 version 3.39[(https://www.nsnam.org)](https://www.nsnam.org/)
* 5G-LENA module version 2.5.y [(https://5g-lena.cttc.es)](https://5g-lena.cttc.es/)
* Bash (or equivalent)
* Python 3.10+
  Libraries required (listed in [python_requirements.txt](/python_requirements.txt)):
  * Pandas
  * Scapy
  * Matplotlib
  * Numpy
  * Seaborn

### Installing and setting up variables

* Install ns3, 5G-LENA and Python
* Copy the repository to `/YOUR_PATH/ns-3-dev/scratch/`

#### Setup

1. Create a copy of the file [paths_default.cfg](/paths_default.cfg), rename it to `paths.cfg`, and change the value of the variable `RUTA_NS3` to the path of the folder where the `ns3` executable is located in your machine.
2. Run the following command, which copies some modified files from the folder [to_replace_in_src](/to_replace_in_src/) to their respective places inside `ns-3-dev/src` and `ns-3-dev/contrib/nr/model`.

```bash
bash copy-mod-files.sh
```

3. Create the directory `out` inside the main folder (this is where the output files will be saved).
4. Install the libraries needed by Python running the command

```bash
pip install -r python_requirements.txt
```

**Note:** the scripts all call the command `python 3` when plotting.

### Running the simulations

There are 3 ways to run the simulation, the first one consists of calling the `ns3` executable with the run keyword and [simulation-main.cc](/sim/simulation-main.cc) as the argument. The second one uses the bash script [run-simulation.sh](/run-simulation.sh), which runs a single simulation instance. The last one is using [parallel.sh](/parallel.sh) which runs multiple simulations in parallel (related to the number of cores in the machine).

The simulation (.cc file) and the bash scripts contain multiple possible arguments, which can be shown using `--help` or `-h`.

#### Single simulation

* Using the bash script, it is necessary to run the following command

```bash
bash run-simulation.sh -c "My_First_Simulation"
```

The output files and generated plots will be saved in `./out/My_First_Simulation/`

#### Batch of simulations (in parallel)

The number of maximum simulations to be run in parallel is determined by the number of CPU cores - 1 in your machine. The arguments that will be given to the simulation are defined inside the file ([parallel.sh](/parallel.sh)) in an array.
To run use the following command:

```bash
bash parallel.sh -c "MyFirstParallelRun"
```

The output files for all the simulations will be saved in `./out/MyFirstParallelRun/`

## Help

Some combination of arguments can cause errors to occur inside the simulation, caused by ns-3 bugs, we tried to circumvent or solve most of them. In case you find a new one we recommend searching or asking in their respective Google groups [ns-3](https://groups.google.com/g/ns-3-users) [5G-LENA](https://groups.google.com/g/5g-lena-users).

## Authors

The emails of all the authors can be found in the paper headline, other ways to contact the corresponding authors (who developed the code) are:

**Agustín González**
GitHub: [@SirCrocker](https://github.com/SirCrocker)

**Diego Torreblanca**
GitHub: [@diegolozo](https://github.com/diegolozo)

**Jorge Ignacio Sandoval**
GitHub: [@sandjorge](https://github.com/sandjorge)

## Academic publication
A. González, D. Torreblanca, J. I. Sandoval, M. Marín and C. Azurdia, "Performance Evaluation of Link Adaptation Algorithms in 5G NR," 2023 IEEE CHILEAN Conference on Electrical, Electronics Engineering, Information and Communication Technologies (CHILECON), Valdivia, Chile, 2023, pp. 1-6, doi: 10.1109/CHILECON60335.2023.10418696. keywords: {5G mobile communication;Heuristic algorithms;Software algorithms;Throughput;Delays;Behavioral sciences;Standards;Adaptive modulation and coding (AMC);block error rate (BLER);link adaptation;mmWave;ns-3 discrete-event network simulator;5G NR network simulations;open-source},
(https://ieeexplore.ieee.org/document/10418696)

## Version History

* 0.1
  * Initial Release

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
