# OpenSpace Lab Solution to the IROS 2026 Indoor Exploration Competition

[![arXiv](https://img.shields.io/badge/arXiv-2610.01505-b31b1b.svg)](https://arxiv.org/abs/2610.01505)

Technical report of **OpenSpace Lab** at the [Competition on Intelligent Information Gathering for Single and Multi-Robot Systems](https://github.com/BYU-FROST-Lab/indoor-exploration-competition), IROS 2026.

The robot has a step budget, and the map counts only after it is uploaded from within communication range of the base. We treat the return trip as part of the decision, not as a score computed after the run.

[**Paper (PDF)**](https://arxiv.org/pdf/2610.01505) · [**arXiv**](https://arxiv.org/abs/2610.01505)

## Results

| Track | Rank | Coverage |
| --- | ---: | ---: |
| Single-Robot Public | **1 / 5** | **61.04%** |
| Single-Robot Private | 3 / 10 | 39.53% |
| Multi-Robot Private | 3 / 10 | 39.91% |

- On large public maps, 49.81% versus 46.28% for the second-place team.
- 1st on the medium-scale single-robot private maps, at 42.53%.

Preliminary numbers are on the seven public maps. Final numbers are a single submission on ten private maps.

## Method

**Single robot.** A pretrained map-completion model proposes which regions are worth visiting. A short beam search orders those regions under the remaining step budget, charging for travel, for topological risk, and for the steps required to get home. Local planning then checks the chosen target against what the robot can actually see, and switches immediately if the target is no longer worth it. The homing rule fires when the remaining budget drops below the estimated return cost plus a small margin. How aggressive the planner is depends on the budget: 1,000, 1,500, or 2,000 steps.

**Multiple robots.** The same local explorer is shared across the team. Targets are scored by information gain and path cost, and penalized when they sit near a teammate's current position, stated intent, or recent trajectory. Agents leave the base in different directions. When one robot is holding too many unreported cells and a teammate is closer to the base, it hands the data off instead of walking all the way back itself.

A longer paper, with the full algorithm, is in preparation.

## Code

This repository is the project page for the public report.

The competition code will be released with the full manuscript, at the address given in the paper:

`https://github.com/OpenSpace-Lab/Indoor-Exploration-IROS2026`

## Citation

```bibtex
@article{zhang2026openspace,
  title   = {OpenSpace Lab Solution to the {IROS} 2026 Indoor Exploration Competition},
  author  = {Zhang, Yuxuan and Li, Dong and Sun, Zezhou and Xu, Yuxuan and Teng, Siyu and Li, Yuchen and Yang, Jianjian and Chen, Long},
  journal = {arXiv preprint arXiv:2610.01505},
  year    = {2026},
  url     = {https://arxiv.org/abs/2610.01505}
}
```

## Team

| Author | Affiliation |
| --- | --- |
| **Yuxuan Zhang** | China University of Mining and Technology, Beijing |
| Dong Li | Macau University of Science and Technology; Institute of Automation, Chinese Academy of Sciences |
| Zezhou Sun | Mohamed bin Zayed University of Artificial Intelligence |
| Yuxuan Xu | China University of Mining and Technology, Beijing |
| Siyu Teng | Shenzhen University |
| Yuchen Li | Technical University of Munich |
| Jianjian Yang | China University of Mining and Technology, Beijing |
| Long Chen | China University of Mining and Technology, Beijing; Institute of Automation, Chinese Academy of Sciences |

Competition organized by Seungchan Kim and Brady Moon, with the IROS 2026 workshop on intelligent information gathering.
