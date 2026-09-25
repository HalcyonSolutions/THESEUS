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

#### THESEUS Dataset Releases

| Dataset | Description | Resource |
| --- | --- | --- |
| **KINSHIP** | Small controlled navigation-ready KGQA benchmark with 1–3 hop questions, annotated reference reasoning paths, and controlled paraphrases | [Hugging Face](https://huggingface.co/datasets/HalcyonSolutions/Kinship) · [GCS mirror](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/Kinship/index.html) |
| **MQuAKE-ST** | Large static navigation-ready variant of MQuAKE with 1–4 hop questions, a fixed Wikidata-derived graph, verified relation-chain templates, paraphrases, and single- and multi-answer settings | [Hugging Face](https://huggingface.co/datasets/HalcyonSolutions/MQuAKE-ST) · [GCS mirror](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/MQuAKE_ST/index.html) |

The released datasets use explicit topic entities and materialized KGs so that
both terminal-answer quality and executed graph trajectories can be evaluated
under a reproducible navigation setting.

#### Additional Navigation-Ready Benchmarks

We also provide navigation-ready versions of established multi-hop KGQA
benchmarks used in our experiments and subsequent evaluations. These datasets
were **not created by the THESEUS authors**. The original dataset sources are
linked below alongside the corresponding THESEUS-formatted versions.

| Dataset | Original source | THESEUS version |
| --- | --- | --- |
| **MetaQA** | [yuyuz/MetaQA](https://github.com/yuyuz/MetaQA) | [GCS](https://storage.googleapis.com/halcyon_data/multihop_ds/datasets/MetaQA/index.html) |
| **PathQuestion** | [zmtkeke/IRN – PathQuestion](https://github.com/zmtkeke/IRN/tree/master/PathQuestion) | Coming soon |
| **WC2014** | [zmtkeke/IRN – WC2014](https://github.com/zmtkeke/IRN/tree/master/WC2014) | Coming soon |

> **Dataset attribution.** The entries above retain their original authorship
> and licensing. The THESEUS versions refer only to preprocessing, encoding,
> and/or repackaging performed to make the datasets compatible with the common
> graph-navigation format used by this project. Please cite the original
> dataset publications when using these benchmarks.

### Adapted Navigation Models

| Model | Navigation paradigm | THESEUS implementation |
| --- | --- | --- |
| **MINERVA** | Reinforcement-learning graph navigation | [HalcyonSolutions/MINERVA](https://github.com/HalcyonSolutions/MINERVA) |
| **MultiHopKG** | Reinforcement-learning graph navigation adapted from MultiHopKG | [HalcyonSolutions/MultiHopKG-NLP](https://github.com/HalcyonSolutions/MultiHopKG-NLP) |
| **SQUIRE** | Sequence-to-sequence path generation | [HalcyonSolutions/SQUIRE](https://github.com/HalcyonSolutions/SQUIRE) |

### Pretrained Checkpoints

Pretrained checkpoints corresponding to the experiments reported in the paper
are provided below.

Each released checkpoint page provides the model archives, saved run
configurations, evaluation artifacts, SHA-256 checksums, and licensing
information.

| Model | KINSHIP | MQuAKE-ST Single | MQuAKE-ST Multi | MetaQA |
| --- | :---: | :---: | :---: | :---: |
| **MINERVA** | [Available](https://storage.googleapis.com/halcyon_data/multihop_ds/conferences/all/minerva/kinshiphinton/index.html) | [Available](https://storage.googleapis.com/halcyon_data/multihop_ds/conferences/all/minerva/mquake_st/single_answers/index.html) | [Available](https://storage.googleapis.com/halcyon_data/multihop_ds/conferences/all/minerva/mquake_st/multi_answers/index.html) | [Available](https://storage.googleapis.com/halcyon_data/multihop_ds/conferences/all/minerva/metaqa/index.html) |
| **MultiHopKG** | Coming soon | Coming soon | Coming soon | Coming soon |
| **SQUIRE** | Coming soon | Coming soon | Coming soon | Coming soon |

The checkpoint archives preserve the trained model together with the effective
configuration and evaluation artifacts from the corresponding experimental run.
See the individual checkpoint pages for archive contents, loading instructions,
checksums, and license information.

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

| Dataset | Entities | Relations | Triples | QA setting | Hop lengths | Reference paths |
| --- | ---: | ---: | ---: | --- | :---: | :---: |
| **KINSHIP** | 24 | 12 | 112 | Single-answer | 1–3 | Yes |
| **MQuAKE-ST** | 38,516 | 665 | 724,141 | Single- and multi-answer | 1–4 | Yes |
| **MetaQA** | 43,234 | 9 | 134,741 | Multi-answer | 1-3 | **No** |

For **KINSHIP** and **MQuAKE-ST**, 1-hop questions are reserved for training in
the mixed-hop setting. These releases include explicit reference reasoning paths,
enabling evaluation of both terminal-answer correctness and executed trajectory
fidelity.

**MetaQA** provides question-answer supervision but does not include reference
reasoning paths.

See the individual dataset pages for construction and preprocessing details,
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
