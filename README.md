# Collaborative AI Agents and Critics for Fault Detection and Cause Analysis in Network Telemetry

[![arXiv](https://img.shields.io/badge/arXiv-2604.00319-b31b1b.svg)](https://arxiv.org/abs/2604.00319) [<img src="https://github.com/user-attachments/assets/d8bc1723-cd4f-4a55-92ed-44270dad0035" height="30" alt="SheQAI Research"/>](https://sheqai.com)

## Authors
**Syed Eqbal Alam**
1. Department of Electrical and Computer Engineering, University of Alberta,
Edmonton, Alberta, Canada

2. SheQAI Research, Edmonton, Alberta, Canada

**Zhan Shu**
1. Department of Electrical and Computer Engineering, University of Alberta,
Edmonton, Alberta, Canada.

---

## Overview

This work presents stochastic iterative algorithms for collaborative control of Artificial Intelligence (AI) agents
and critics in a **federated multi-agent system**. Each AI agent and critic has access to
classical machine learning models and generative AI foundation models. Agents complete
multimodal tasks and send their responses to critics for evaluation; critics send feedback
to agents to iteratively improve responses. Collaboratively, agents and critics minimize the
overall system cost—with **no inter-agent or inter-critic communication** and with private cost
functions.

The developed solution is demonstrated on **fault detection, severity classification, and root cause
analysis** using a real-world open-source network telemetry dataset.

---

## Key Contributions

-  **Stochastic iterative algorithms** for collaborative control of multiple AI agents and
  critics in a federated multi-agent system, leveraging both classical ML and generative AI
  foundation models
- **Convergence guarantees** on the time-average active states of AI agents and critics,
  via multi-time scale stochastic approximation with generalized decreasing step sizes
-  **Privacy-preserving design** — agents and critics keep their cost functions and
  derivatives private; no inter-agent or inter-critic communication is required
-  **Low communication overhead** — scales as $$O(m)$$ for $$m$$ modalities, independent of the number of agents and critics
-  **Real-world evaluation** on a network telemetry dataset with tabular CSV data and
  log files covering optical transceiver events, admin state changes, and fiber optic link
  state changes.

---

## Abstract

We develop algorithms for collaborative control of AI agents and critics in a multi-actor,
multi-critic federated multi-agent system. Each AI agent and critic has access to classical
machine learning or generative AI foundation models. The AI agents and critics collaborate
with a central server to complete multimodal tasks such as fault detection, severity, and
cause analysis in a network telemetry system, text-to-image generation, video generation,
healthcare diagnostics from medical images and patient records, etcetera.
The AI agents complete their tasks and send them to AI critics for evaluation. The critics
then send feedback to agents to improve their responses. Collaboratively, they minimize the
overall cost to the system with no inter-agent or inter-critic communication. AI agents and
critics keep their cost functions or derivatives of cost functions private.
Using multi-time scale stochastic approximation techniques, we provide convergence guarantees
on the time-average active states of AI agents and critics. The communication overhead is of
the order of $$O(m)$$, for $$m$$ modalities, and is independent of the number of AI agents and
critics. Finally, we present an example of fault detection, severity, and cause analysis in
network telemetry and thorough evaluation to check the algorithm's efficacy.

**Index Terms:** AI agents, distributed optimization, optimal control, multimodal foundation
models, generative AI, federated multi-agent system, large language models.

---

## System Architecture

> *Figure 1: Block diagram of AI agent–critic interaction. Agents generate responses and
> send them to critics; critics evaluate and return feedback.*

<img width="973" alt="Agent-Critic Block Diagram" src="https://github.com/user-attachments/assets/c71fc6ea-cccb-4f85-8c45-3a6e18a54a48" />

> *Figure 4: Federated multi-agent system. AI agents and critics coordinate with a central
> server that broadcasts feedback signals $$\Theta_j$$ and $$\Theta^c_j$$ for each modality at every time step.*

<img width="817" alt="Federated Multi-Agent System Block Diagram" src="https://github.com/user-attachments/assets/9245002d-daa9-4380-8c25-e347f89ec674" />

---

## Experimental Setup

Experiments use **Dataset 4** from the open-source network telemetry benchmark of 
[Putina & Rossi, IEEE TNSM 2021](https://github.com/cisco-ie/telemetry), which contains:

- Tabular CSV data with 99 columns (numeric and non-numeric), including bandwidth,
  bytes-received, bytes-sent, CRC-errors, input-data-rate, input-drops, reliability, etc.
- Log files for three types of port state changes: optical transceiver pull/reinsert, admin
  state change (down/up), and link state changes (fiber optic plug-in/plug-out)

**Configuration:** 9 agents, 2 modalities (CSV telemetry data + fault query logs), 3 critics
per modality, desired active critics per modality = 2.

**Models used:** Llama3.2, DeepSeek-R1, Mistral, Llava:7b, IBM Granite3.2:8b, and
Microsoft Phi4:14b — all open-source, deployed via Ollama and integrated via LangChain.

**Hardware:** Intel Core i9, 2.20 GHz, 32 GB RAM, NVIDIA GeForce RTX 4080.

**Fault detection** is evaluated using two approaches:
- Agents enabled with **XG Boosting** (classical ML)
- Agents and critics enabled with **LLMs**, with and without Retrieval Augmented
  Generation (RAG) via ChromaDB and mxbai-embed-large embeddings

**Fault severity and cause analysis** uses LLM-enabled agents and critics, with access to
vector-embedded network telemetry log files stored in ChromaDB.

---

## Selected Results

### Fault Detection Performance

| Model | Accuracy | Precision | Recall | F1-Score |
|-------|----------|-----------|--------|----------|
| Agents with XG Boosting | **0.9644** | **0.9397** | **0.9929** | **0.9656** |
| Agents & Critics with Llama3.2 (with RAG) | 0.5882 | 0.8000 | 0.6154 | 0.6957 |
| Agents & Critics with Llama3.2 (without RAG) | 0.4612 | 0.4027 | 0.6648 | 0.5016 |

> XG Boosting-enabled agents outperform LLM-enabled agents on fault detection accuracy,
> F1-score, precision, and recall — with faster execution. LLM-enabled agents and critics
> are used for the subsequent fault severity and cause analysis step.

### Convergence and System Cost

> *Figures below show convergence of agent and critic time-average active states,
> and the evolution of the total cost ratio (developed algorithm vs. CVX
> centralized solver) converging close to 1.*

 <img width="1139" height="560" alt="image" src="https://github.com/user-attachments/assets/d782dcc6-5ef0-40de-a953-da67bf280d28" />

<img width="1088" height="480" alt="image" src="https://github.com/user-attachments/assets/02efec86-007d-4d81-943f-bfcf8fb2ca0a" />


### Fault Severity Classification by Large Language Models

> *Proportion of faults classified as Critical vs. Non-critical by each LLM. Llama3.2
> classifies the highest proportion as critical (25.8%); IBM Granite3.2:8b classifies the least
> (0.1%).*
<img width="788" alt="Convergence and cost results" src="https://github.com/user-attachments/assets/8889387e-90ac-4956-95ef-8a7a6c57932a" />

<img width="816" alt="Fault severity pie charts and UpSet plot" src="https://github.com/user-attachments/assets/94454142-e603-4727-b287-b095dc80028b" />

---

## Citation

Please cite the work, if it is useful to you:
```bibtex
@misc{alam2026collaborativeaiagentscritics,
      title={Collaborative AI Agents and Critics for Fault Detection and Cause Analysis in Network Telemetry},
      author={Syed Eqbal Alam and Zhan Shu},
      year={2026},
      eprint={2604.00319},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2604.00319},
}
```
## Dataset References
> Andrian Putina and Dario Rossi. Online anomaly detection leveraging stream-based
clustering and real-time telemetry. IEEE Transactions on Network and Service Management,
18(1):839–854, 2021, https://github.com/cisco-ie/telemetry.


## Acknowledgements

> This research work is partially supported by **SheQAI Research**, and the
**University of Alberta–Huawei Joint Innovation Centre** (project number ZAI7F).

> A part of the README is created by Anthropic's Claude.

## Paper
**[Collaborative AI Agents and Critics for Fault Detection and Cause Analysis in Network Telemetry](https://arxiv.org/abs/2604.00319)**
arXiv:2604.00319 [cs.AI], March 2026.

---------
