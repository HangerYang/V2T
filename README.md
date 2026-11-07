# V2T: Distilling Visual Reasoning into Text Space

[Wenhan Yang](https://hangeryang.github.io/), Nilay Naharas, Ali Payani, [Baharan Mirzasoleiman](https://baharanm.github.io/) · UCLA and Cisco Research

[Project page](https://hangeryang.github.io/V2T/) · [Paper](https://arxiv.org/abs/2609.34408)

Models that "think with images" generate intermediate images or latent visual tokens inside their chain of thought. That is slow, the generated visuals can be wrong, and interleaved images increasingly interfere with the text reasoning itself. **V2T** uses interleaved images only as training-time supervision:

1. **Interleaved teacher.** Fine-tune on chains of thought whose steps come with reasoning images (crops, zooms, constructions).
2. **Text-only student.** Distill into a student that sees only the problem image, using the teacher's logits, ground-truth text and, when reasoning images map back to the original image, the teacher's attention on the matching region.
3. **Optional short GRPO.** A brief RL run, with a grounding reward for attending to the right region when boxes are available.

At inference the student reasons in text alone, at the same cost as any text-only model.

| | Broad visual suite avg. | Training GPU-hours | Inference cost |
|---|---|---|---|
| Vision-R1-7B | 59.1 | 3,392 | 1× |
| DeepEyes (tool-based) | 59.1 | 1,536 | 45× |
| LVR-7B (latent visual) | 56.7 | 160 | 2× |
| **V2T** | **61.8** | **20** | **1×** |
| **V2T + GRPO** | **63.4** | **80** | **1×** |

The broad suite covers HR-Bench 4K/8K, V*Bench, BLINK and POPE. On visual math, V2T + GRPO trained on ViRC reaches **73.3 on MathVista**, the highest among the 7B reasoning models compared. Full results are on the [project page](https://hangeryang.github.io/V2T/).

Code is coming soon.

## Citation

```bibtex
@article{yang2026distilling,
  title   = {Distilling Visual Reasoning into Text Space},
  author  = {Yang, Wenhan and Naharas, Nilay and Payani, Ali and Mirzasoleiman, Baharan},
  journal = {arXiv preprint arXiv:2609.34408},
  year    = {2026}
}
```
