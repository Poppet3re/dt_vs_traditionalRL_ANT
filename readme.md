# Decision Transformers vs Traditional Offline RL: A Study Using the ANT Environment

This repository contains the implementation of experiments comparing Decision Transformers (DT), Conservative Q-Learning (CQL), and Implicit Q-Learning (IQL) in dense vs. sparse reward settings using the ANT environment.

## Abstract

This study evaluates the performance of Decision Transformers against traditional offline RL algorithms (CQL and IQL) in dense and sparse reward settings, focusing on the ANT environment - a complex continuous control task. Our research investigates how these algorithms perform when faced with different reward structures, examining their ability to learn effective policies and generalize across varying levels of feedback.

## Repository Structure
```
.
├── requirements.txt
├── DT/
│   ├── dt_dense.py
│   └── dt_sparse.py
├── CQL/
│   ├── cql_dense.py
│   └── cql_sparse.py
└── IQL/
    ├── iql_dense.py
    └── iql_sparse.py
```

## Installation

### 1. MuJoCo Installation (Ubuntu 22.04)

First, install the required system dependencies:
```bash
sudo apt-get update && sudo apt-get install -y \
    libgl1-mesa-dev \
    libgl1-mesa-glx \
    libglew-dev \
    libosmesa6-dev \
    software-properties-common \
    net-tools \
    vim \
    wget \
    unzip \
    git
```

Download and install MuJoCo 2.1.0:
```bash
mkdir -p ~/.mujoco
wget https://github.com/deepmind/mujoco/releases/download/2.1.0/mujoco210-linux-x86_64.tar.gz
tar -xf mujoco210-linux-x86_64.tar.gz -C ~/.mujoco/
rm mujoco210-linux-x86_64.tar.gz
```

Add MuJoCo to your PATH by adding these lines to your `~/.bashrc`:
```bash
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:~/.mujoco/mujoco210/bin
export LD_PRELOAD=/usr/lib/x86_64-linux-gnu/libGLEW.so
```

Apply the changes:
```bash
source ~/.bashrc
```

### 2. Python Environment Setup

#### Using Miniconda (Recommended)
```bash
# Install Miniconda (if not already installed)
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

# Create and activate environment
conda create -n ant_rl python=3.8
conda activate ant_rl

# Install requirements
pip install -r requirements.txt
pip install "cython<3"
```

#### Using venv (Alternative)
```bash
python -m venv ant_rl
source ant_rl/bin/activate
pip install -r requirements.txt
pip install "cython<3"
```

## Running the Experiments

Each algorithm (DT, CQL, IQL) has separate files for dense and sparse reward settings. To run an experiment:

1. Activate your environment:
```bash
conda activate ant_rl  # or source ant_rl/bin/activate for venv
```

2. Run the desired experiment:
```bash
python CQL/cql_dense.py  # for CQL with dense rewards
python DT/dt_sparse.py   # for DT with sparse rewards
# etc.
```

To modify the environment, edit the `env_name` variable in the respective Python files. Available environments include:
- ant-medium-v2
- ant-medium-replay-v2
- ant-medium-expert-v2
- ant-expert-v2

## Key Findings

Our experiments revealed several important insights:

1. **Performance Across Reward Structures**: 
   - Decision Transformers show consistent performance across both sparse and dense rewards
   - Traditional methods (CQL, IQL) generally perform better with dense rewards

2. **Dataset Quality Impact**:
   - All algorithms improve with higher quality datasets
   - DT excels with medium-expert datasets in sparse reward settings
   - IQL shows impressive results with high-quality data in dense reward environments

3. **Computational Efficiency**:
   - DT: ~7.5 hours training time
   - CQL: ~5 hours training time
   - IQL: ~2 hours training time

For detailed results and analysis, please refer to the full paper.

## Citation

If you use this code in your research, please cite:
```bibtex
@article{caunhye2024decision,
  title={Decision Transformers vs Traditional Offline Reinforcement Learning Algorithms in Dense vs. Sparse Reward Settings: A Study Using the ANT Environment},
  author={Caunhye, Ali Murtaza and Jeewa, Asad},
  year={2024}
}
```
