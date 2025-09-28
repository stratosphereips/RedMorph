# RedMorph: Characterizing the Challenges of Attacker Adaptation in Realistic Networks

This repository contains the code, experiments, and supporting material for the paper:

**RedMorph: Characterizing the Challenges of Attacker Adaptation in Realistic Networks**  
*Stratosphere Laboratory, September 2025*

---

## 📖 Overview

RedMorph investigates the **generalization problem of autonomous attacker agents** in cybersecurity environments.  
We study how agents can adapt their learned policies when facing **new, unseen network topologies**, focusing on:

- Data exfiltration attack scenarios
- Bridging the gap between **theory** and **realism**
- Comparing different adaptation and generalization strategies

Our contributions include:

- A redesigned **NetSecGame** environment with changing topologies
- A systematic **training/evaluation methodology** for attacker adaptation
- Evaluation of multiple agents:
  - **Deep Q-Networks (DQN)**
  - **Model-Agnostic Meta Learning (MAML)**
  - **Conceptual Q-learning/SARSA (state abstraction)**
  - **Large Language Model (LLM)-based agents**
- An **XAI framework** to analyze action distributions and explain generalization

---

## 🧩 Problem Statement

Most attacker agents in cybersecurity simulations **fail to transfer knowledge** when network topology changes.  
We ask:

- Can attackers learn **abstract, general policies**?  
- How well do different RL/meta-RL/LLM agents **adapt to unseen networks**?  
- Can we explain **why and how** agents generalize using interpretable methods?

---

## 🛠 Environment: NetSecGame (NSG)

We extend **NetSecGame**, a multi-agent security environment.

- **Observation Space:** networks, hosts, services, data, firewall rules  
- **Action Space:**  
  - `ScanNetwork`, `FindServices`, `FindData`, `ExploitService`, `ExfiltrateData`, `BlockIP`  
- **Scenario:** Data exfiltration  
  - Compromise internal hosts  
  - Find and access the target server  
  - Exfiltrate data to a C&C server  

---

## 🤖 Agents Implemented

### 1. **DQN**
- Classic Deep Q-Learning attacker  
- Single-buffer and dual-buffer variants  
- Candidate-centric 12D state representation  

### 2. **MAML**
- Meta-RL attacker using Model-Agnostic Meta Learning  
- Learns initialization for **fast adaptation** to unseen topologies  

### 3. **Conceptual Agent**
- Abstraction-based Q-learning agent  
- Uses **concepts** (roles, functions) instead of raw values (IP addresses, services)  

### 4. **LLM Agents**
- GPT-4o-mini and Gemma-3 evaluated as **reasoning-based attackers**  

---

## 📊 Results Summary

- Agents trained on 5 topologies, tested on a 6th unseen topology  
- Average **generalization success ~65–70%** across agents  
- Key insights:
  - **Conceptual abstraction** enables broader transfer
  - **MAML** improves zero-shot adaptation
  - **LLMs** show promise but require careful integration
  - **DQN** struggles when evaluation topology diverges from training

---

## 🔍 Explainability (XAI)

We analyze **action distributions over time** to understand strategies:  

- Q-learning vs. Conceptual Q-learning  
- MAML adaptation vs. LLM strategies  
- Insights into **how different agents explore, exploit, and exfiltrate** in new environments  

---

## 📂 Repository Structure

```
.
├── figures/           # Plots, environment diagrams, agent results
├── src/               # Agent implementations
│   ├── dqn/
│   ├── maml/
│   ├── conceptual/
│   └── llm/
├── env/               # NetSecGame modifications
├── experiments/       # Training & evaluation scripts
├── notebooks/         # Analysis & visualization
└── paper/             # LaTeX source of the paper
```

---

## 🚀 Getting Started

### Requirements
- Python 3.10+
- PyTorch
- Gym-like environment (custom NetSecGame)
- Transformers (for LLM agents)
- Matplotlib / Seaborn (for plotting)

### Installation
```bash
git clone https://github.com/stratosphere-lab/RedMorph.git
cd RedMorph
pip install -r requirements.txt
```

### Running an Experiment
```bash
python experiments/train_dqn.py --topologies data/topos --episodes 1000
python experiments/eval_dqn.py --model checkpoints/dqn.pth --topology data/test_topo.json
```

### Reproducing Paper Results
- See [notebooks/](notebooks/) for evaluation and XAI plots.  

---

## 📜 Citation

If you use this code or dataset, please cite:

```
@article{redmorph2025,
  title={RedMorph: Characterizing the Challenges of Attacker Adaptation in Realistic Networks},
  author={Stratosphere Laboratory CTU University, UTEP University},
  year={2025},
  journal={arXiv preprint}
}
```

---

## 🔗 References

- NetSecGame: [GitHub Repository](https://github.com/stratosphere-lab/netsecgame)  
- MAML: Finn et al., *ICML 2017*  
- Related cyber-RL works: Collyer (2022), Applebaum (2022), Janisch (2023), Wolk (2022)

---

## 📬 Contact

Stratosphere Laboratory  
[https://www.stratosphereips.org](https://www.stratosphereips.org)  
