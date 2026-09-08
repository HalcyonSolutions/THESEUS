# THESEUS

## Theseus in the Graph: Towards Traceable Multi-Hop Graph Navigation

**THESEUS** studies multi-hop Knowledge Graph Question Answering (KGQA) as
**question-conditioned graph navigation**.

Given a natural-language question, a topic entity, and a knowledge graph, an
agent must navigate the graph to reach a valid answer while producing the
explicit sequence of relations and entities used to get there.

The goal is to evaluate not only **whether a model reaches the correct answer**,
but also **whether its trajectory follows the intended reasoning structure**.

> **Paper:** *Theseus in the Graph: Towards Traceable Multi-Hop Graph Navigation*  
> Eduin E. Hernandez, Luis F. Garcia, Nurassyl Askar, Sergio A. Diaz, Stefano Rini  
> **Preprint:** link coming soon

---

## Resources

This repository is the central landing page for the datasets, adapted models,
checkpoints, and evaluation resources used in THESEUS.

### Datasets

| Dataset | Description | Resource |
| --- | --- | --- |
| **KINSHIP** | Small controlled KGQA benchmark with 1–3 hop questions, annotated reasoning paths, and paraphrased questions | [Dataset](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/Kinship/index.html) |
| **MQuAKE-ST** | Static navigation-ready variant of MQuAKE with 1–4 hop questions, annotated paths, paraphrases, and single- and multi-answer settings | [Dataset](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/MQuAKE_ST/index.html) |

### Adapted Navigation Models

| Model | Navigation paradigm | THESEUS implementation |
| --- | --- | --- |
| **MINERVA** | Reinforcement-learning graph navigation | [HalcyonSolutions/MINERVA](https://github.com/HalcyonSolutions/MINERVA) |
| **MultiHopKG** | Reinforcement-learning graph navigation adapted from MultiHopKG | [HalcyonSolutions/MultiHopKG-NLP](https://github.com/HalcyonSolutions/MultiHopKG-NLP) |
| **SQUIRE** | Sequence-to-sequence path generation | [HalcyonSolutions/SQUIRE](https://github.com/HalcyonSolutions/SQUIRE) |

### Pretrained Checkpoints

Pretrained checkpoints corresponding to the experiments reported in the paper
will be linked here.

| Model | KINSHIP | MQuAKE-ST Single | MQuAKE-ST Multi |
| --- | :---: | :---: | :---: |
| MINERVA | Coming soon | Coming soon | Coming soon |
| MultiHopKG | Coming soon | Coming soon | Coming soon |
| SQUIRE | Coming soon | Coming soon | Coming soon |

---

## What is THESEUS?

Traditional multi-hop KGQA evaluation primarily asks whether a system predicts
the correct answer. THESEUS instead treats reasoning as an explicit navigation
problem:

```text
Natural-language question
          +
     Topic entity
          +
    Knowledge graph
          |
          v
 Question-conditioned
   navigation policy
          |
          v
e0 --r1--> e1 --r2--> ... --rn--> answer
          |
          v
Answer correctness + Path traceability
