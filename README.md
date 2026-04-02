# Collaborative AI Agents and Critics for Fault Detection and Cause Analysis in Network Telemetry

## Authors and Affiliations

**Syed Eqbal Alam**
1. Department of Electrical and Computer Engineering, University of Alberta,
Edmonton, Alberta, Canada
2. SheQAI Research, Edmonton, Alberta, Canada
   
**Zhan Shu**
1. Department of Electrical and Computer Engineering, University of Alberta,
Edmonton, Alberta, Canada.

# Abstract
We develop algorithms for collaborative control of AI agents and critics in a multiactor,
multi-critic federated multi-agent system. Each AI agent and critic has access to classical
machine learning or generative AI foundation models. The AI agents and critics collaborate with a
central server to complete multimodal tasks such as fault detection, severity, and cause analysis in a
network telemetry system, text-to-image generation, video generation, healthcare diagnostics from
medical images and patient records, etcetera. The AI agents complete their tasks and send them
to AI critics for evaluation. The critics then send feedback to agents to improve their responses.
Collaboratively, they minimize the overall cost to the system with no inter-agent or inter-critic
communication. AI agents and critics keep their cost functions or derivatives of cost functions
private. Using multi-time scale stochastic approximation techniques, we provide convergence guarantees
on the time-average active states of AI agents and critics. The communication overhead is a
little on the system, of the order of O(m), for m modalities and is independent of the number of AI
agents and critics. Finally, we present an example of fault detection, severity, and cause analysis
in network telemetry and thorough evaluation to check the algorithm’s efficacy.


### System's block diagram
<img width="973" height="691" alt="image" src="https://github.com/user-attachments/assets/c71fc6ea-cccb-4f85-8c45-3a6e18a54a48" />


<img width="817" height="1009" alt="image" src="https://github.com/user-attachments/assets/9245002d-daa9-4380-8c25-e347f89ec674" />

### Selected results on Fault detection and cause analysis in a multimodal network telemetry system
<img width="788" height="543" alt="image" src="https://github.com/user-attachments/assets/8889387e-90ac-4956-95ef-8a7a6c57932a" />

<img width="816" height="516" alt="image" src="https://github.com/user-attachments/assets/94454142-e603-4727-b287-b095dc80028b" />

------------
## Citation:
```@misc{alam2026collaborativeaiagentscritics,
      title={Collaborative AI Agents and Critics for Fault Detection and Cause Analysis in Network Telemetry}, 
      author={Syed Eqbal Alam and Zhan Shu},
      year={2026},
      eprint={2604.00319},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2604.00319}, 
}
```
