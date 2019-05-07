# HW3 Tester

NOTE: We are using Python 3. Make sure you are too:

```
(hw3) $ python --version
Python 3.6.1 :: Continuum Analytics, Inc.
```

## MH's additional note
1. Use exact versions of all dependencies as specified, Use Python 3.6.1, Python 3.7 will cause error in the plotting function

2. switch to conda env
```
source activate hw3
conda deactivate
```


## Installation:

You can run the testing script 3 different ways:

1. Conda:

```bash
# create conda environment and activate it
conda create -n hw3 python=3
source activate hw3

# install dependencies
conda install numpy pydot networkx progressbar2
pip install pymdptoolbox pygraphviz

# run the script to test the sample mdp
python hw3_tester.py -vvv -m sample.json -i
```

2. Pip:

```bash
pip3 install numpy pydot networkx progressbar2 pygraphviz pymdptoolbox
# or
pip3 install -r requirements.txt
```

### pyraphiz failing to install?
`pygraphviz` requires you to have the graphviz package installed on your OS.
See this [thread](https://github.com/rldm/hw3-tester/issues/2)


3. Docker:

```bash
docker build -t rldm/hw3-tester:v1 .
docker run --privileged=true --rm \
    -v $PWD:/mnt/hw3-tester \
    -it rldm/hw3-tester:v1 /bin/bash
```

On windows using powershell:

```powershell
docker build -t rldm/hw3-tester:v1 .
$WorkingDir = Convert-Path .
docker run --privileged=true --rm -v $WorkingDir\:/mnt/hw3-tester -it rldm/hw3-tester:v1 /bin/bash
```

If you run into permissions errors when the docker container is building, you might have to change the Dockerfile to run the pip command before it resets the user back to the non root user.

If you run the test script in the next section and it gives you trouble about pymdptoolbox not being there, rerun the `pip` command inside the container without using `pip3`, use `pip` instead.

## Testing the script

```bash
python hw3_tester.py -m sample.json -i -vvv
```

Output will show:

```
06/12/2017 01:57:32 AM - INFO: 
06/12/2017 01:57:32 AM - INFO: mdp returned median number of iterations 2
number of iterations: 2
06/12/2017 01:57:32 AM - INFO: end of script
```

An image will be created on the same directory the `json` file.

## Help?

```
python hw3_tester.py -h
usage: hw3_tester.py [-h] [-v] [-vv] [-vvv] -m MDP_PATH [-c] [-i] [-s]

Reinforcement Learning and Decision Making, HW3 Tester

optional arguments:
  -h, --help            show this help message and exit
  -v                    logging level set to ERROR
  -vv                   logging level set to INFO
  -vvv                  logging level set to DEBUG
  -m MDP_PATH, --mdp MDP_PATH
                        Path to the MDP json file
  -c, --check_only      Flag to only check valid MDP on JSON file
  -i, --iterations      Calculate how many iterations PI takes to solve this
  -s, --visualize       Visualize MDP (export to png)
```

