# THESEUS

## Theseus in the Graph: Towards Traceable Multi-Hop Graph Navigation

**THESEUS** studies multi-hop Knowledge Graph Question Answering (KGQA) as
**question-conditioned graph navigation**.

Given a natural-language question, a topic entity, and a knowledge graph, an
agent must navigate the graph to reach a valid answer while producing the
explicit sequence of relations and entities used to get there.

The goal is to evaluate not only **whether a model reaches the correct answer**,
but also **whether its trajectory follows the intended reasoning structure**.

> **Paper:** [*Theseus in the Graph: Towards Traceable Multi-Hop Graph Navigation*](https://arxiv.org/abs/2609.14528)  
> Eduin E. Hernandez, Luis F. Garcia, Nurassyl Askar, Sergio A. Diaz, Stefano Rini  
> **arXiv:** [2609.14528](https://arxiv.org/abs/2609.14528)

---

## Resources

This repository is the central landing page for the datasets, adapted models,
checkpoints, and evaluation resources used in THESEUS.

### Datasets

| Dataset | Description | Resource |
| --- | --- | --- |
| **KINSHIP** | Small controlled navigation-ready KGQA benchmark with 1–3 hop questions, annotated reference reasoning paths, and controlled paraphrases | [Hugging Face](https://huggingface.co/datasets/HalcyonSolutions/Kinship) · [GCS mirror](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/Kinship/index.html) |
| **MQuAKE-ST** | Large static navigation-ready variant of MQuAKE with 1–4 hop questions, a fixed Wikidata-derived graph, verified relation-chain templates, paraphrases, and single- and multi-answer settings | [Dataset](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/MQuAKE_ST/index.html) |

The released datasets use explicit topic entities and materialized KGs so that
both terminal-answer quality and executed graph trajectories can be evaluated
under a reproducible navigation setting.

### Adapted Navigation Models

| Model | Navigation paradigm | THESEUS implementation |
| --- | --- | --- |
| **MINERVA** | Reinforcement-learning graph navigation | [HalcyonSolutions/MINERVA](https://github.com/HalcyonSolutions/MINERVA) |
| **MultiHopKG** | Reinforcement-learning graph navigation adapted from MultiHopKG | [HalcyonSolutions/MultiHopKG-NLP](https://github.com/HalcyonSolutions/MultiHopKG-NLP) |
| **SQUIRE** | Sequence-to-sequence path generation | [HalcyonSolutions/SQUIRE](https://github.com/HalcyonSolutions/SQUIRE) |

### Pretrained Checkpoints

Pretrained checkpoints corresponding to the experiments reported in the paper
will be linked here as they are released.

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
```

THESEUS evaluates both:

- **Answer ranking:** MRR and Hits@1
- **Path traceability:** PED, RED, F1_SG, and F1_Rel

The adapted models replace their original symbolic query interfaces with
natural-language question conditioning while preserving their underlying
navigation architectures. The reasoning horizon is separated from the
underlying question hop length, allowing questions of different depths to be
evaluated under a common traversal budget.

---

## Dataset Summary

| Dataset | Entities | Relations | Triples | QA setting | Hop lengths |
| --- | ---: | ---: | ---: | --- | --- |
| **KINSHIP** | 24 | 12 | 112 | Single-answer | 1–3 |
| **MQuAKE-ST** | 38,516 | 665 | 724,141 | Single- and multi-answer | 1–4 |

For both released datasets, 1-hop questions are reserved for training in the
mixed-hop setting. See the individual dataset pages for construction details,
split statistics, licensing, checksums, and machine-readable metadata.

---

## Citation

If you use THESEUS, the released datasets, or the evaluation protocol, please
cite:

```bibtex
@article{hernandez2026theseus,
  author  = {Hernandez, Eduin E. and Garcia, Luis F. and Askar, Nurassyl and Diaz, Sergio A. and Rini, Stefano},
  title   = {Theseus in the Graph: Towards Traceable Multi-Hop Graph Navigation},
  journal = {arXiv preprint arXiv:2609.14528},
  year    = {2026}
}
```

When using **Kinship (KGQA)**, please also cite the original UCI **Kinship** work listed on the [Kinship_dataset_page](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/Kinship/index.html)

When using **MQuAKE-ST**, please also cite the original **MQuAKE** and
**MQuAKE-Remastered** works as listed on the
[MQuAKE-ST dataset page](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/MQuAKE_ST/index.html).

When using the adapted model implementations, please also cite the
corresponding original **MINERVA**, **MultiHopKG**, or **SQUIRE** paper.
