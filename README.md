<div align="center">
    <h1> <a href="http://blog.goedel-prover.com"> <strong>Goedel-Prover-V2: The Strongest Open-Source Theorem Prover to Date</strong></a></h1>
</div>

<div align="center">
  
[![Website](https://img.shields.io/badge/%F0%9F%A4%96%20Homepage-Goedel-536af5?color=536af5&logoColor=white)](http://blog.goedel-prover.com)
[![Hugging Face](https://img.shields.io/badge/%F0%9F%A4%97%20Hugging%20face-Goedel-ffc107?color=ffc107&logoColor=white)](https://huggingface.co/Goedel-LM/Goedel-Prover-V2-32B)
[![arXiv](https://img.shields.io/badge/arXiv-comming.soon-b31b1b.svg?style=flat)](#)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

 </div>

## 1. Introduction

We introduce Goedel-Prover-V2, an open-source language model series that sets a new state-of-the-art in automated formal proof generation. Built on the standard expert iteration and reinforcement learning pipeline, our approach incorporates three key innovations: (1) <strong>Scaffolded data synthesis</strong>: We generate synthetic proof tasks of increasing difficulty to progressively train the model, enabling it to master increasingly complex theorems; (2) <strong>Verifier-guided self-correction</strong>: The model learns to iteratively revise its own proofs by leveraging feedback from Lean’s compiler, closely mimicking how humans refine their work; (3) <strong>Model averaging</strong>: We combine multiple model checkpoints to improve robustness and overall performance.

Our small model, Goedel-Prover-V2-8B, reaches 83.0% on MiniF2F test set at Pass@32, matching the performance of prior state-of-the-art DeepSeek-Prover-V2-671B while being nearly 100 times smaller in model size.  Our flagship model, Goedel-Prover-V2-32B, achieves 88.0% on MiniF2F at Pass@32 on standard mode and 90.4% on self-correction mode, outperforming prior SOTA DeepSeek-Prover-V2-671B and concurrent work Kimina-Prover-72B by a large margin. Additionaly, our flagship model with self-correction solves 64 problems on PutnamBench at Pass@64, securing the 1st on the leaderboard surpassing DeepSeek-Prover-V2-671B's record of solving 47 problems by Pass@1024.

## 2. Benchmark Performance

<strong>Self-correction mode</strong>: Our model improves proof quality by first generating an initial candidate and then using Lean compiler feedback to iteratively revise it. We perform two rounds of self-correction, which remain computationally efficient—the total output length (including the initial proof and two revisions) increases only modestly from the standard 32K to 40K tokens.

<figure>
  <div class="fig-row">
    <div class="panel panel-1" style="width:100%;">
      <img src="https://github.com/Goedel-LM/Goedel-Prover-V2/blob/main/assets/combined_performance_plots_varied_width.png?raw=true" alt="…">
    </div>
  </div>
  <figcaption>
  <strong>Figure 1</strong>: <em>Pass@32 performance on MiniF2F, PutnamBench, and our new MathOlympiadBench containing 360 IMO-level problems.</em>
  </figcaption>
</figure>

The charts above demonstrate the state-of-the-art performance of Goedel-Prover-V2. We report all numbers at Pass@32: (1) Across all three datasets, our flagship 32B model, in both standard and self-correction mode, significantly outperforms prior state-of-the-art DeepSeek-Prover-V2-671B and Kimina-Prover-72B; (2) on miniF2F, our 8B model matches the performance of DeepSeek-Prover-V2-671B while being 100 times smaller in model size.


<div align="center">
  <table style="margin: 0 auto;">
    <thead>
      <tr>
        <th>#</th>
        <th>Model</th>
        <th>num‑solved</th>
        <th>compute</th>
      </tr>
    </thead>
    <tbody>
      <tr><td>1</td><td><strong>Goedel-Prover-V2-32B (self-correction mode)</strong></td><td><strong>86</strong></td><td><strong>Pass@192</strong></td></tr>
      <tr><td>1</td><td><strong>Goedel-Prover-V2-32B (self-correction mode)</strong></td><td><strong>57</strong></td><td><strong>Pass@32</strong></td></tr>
      <tr><td>1</td><td><strong>Goedel-Prover-V2-32B</strong></td><td><strong>43</strong></td><td><strong>Pass@32</strong></td></tr>
      <tr><td>2</td><td>DeepSeek‑Prover‑V2-671B</td><td>47</td><td>Pass@1024</td></tr>
      <tr><td>2</td><td>DeepSeek‑Prover‑V2-671B</td><td>22</td><td>Pass@32</td></tr>
      <tr><td>3</td><td>DSP+</td><td>23</td><td>Pass@128</td></tr>
      <tr><td>4</td><td>Kimina‑Prover‑7B‑Distill</td><td>10</td><td>Pass@192</td></tr>
      <tr><td>5</td><td>Self-play Theorem Prover</td><td>8</td><td>Pass@3200</td></tr>
      <tr><td>6</td><td>Goedel-Prover-V1</td><td>7</td><td>Pass@512</td></tr>
    </tbody>
  </table>
    <!-- table caption -->
    <caption align="bottom"><strong>Table 1</strong>: <em>PutnamBench leaderboard. Goedel-Prover-V2-32B secures the top rank with significantly less compute (pass number) than the previous state-of-the-art.</em>
</div>

## 3. Compelling Scaling Performance

<figure>
  <div align="center">
    <img
      src="https://github.com/Goedel-LM/Goedel-Prover-V2/blob/main/assets/inference_scale_performance.png?raw=true"
      alt="Performance on MiniF2F under different sample budgets"
      width="60%"
    />
  </div>
  <figcaption>
    <strong>Figure 2</strong>: <em>Performance on MiniF2F test set under different sample budgets.</em>
  </figcaption>
</figure>

The scaling curves above show that our 32B model consistently outperforms all prior state-of-the-art models across the entire range of inference-time compute budgets.

## 4. Model & Dataset Downloads

We release our Goedel-Prover-V2 models and the new MathOlympiadBench benchmark to foster future research.

<div align="center">
  
| Model | Download |
| -------- | -------- |
|    Goedel-Prover-V2-32B    |   [🤗Download](https://huggingface.co/Goedel-LM/Goedel-Prover-V2-32B)    |
|    Goedel-Prover-V2-8B    |   [🤗Download](https://huggingface.co/Goedel-LM/Goedel-Prover-V2-8B)    |

</div>

<div align="center">

| Dataset | Download |
| -------- | -------- |
|    MathOlympiadBench    |   [🤗Download](https://huggingface.co/datasets/Goedel-LM/MathOlympiadBench)    |

</div>

<strong>MathOlympiadBench</strong> (Math Olympiad Bench) comprises human-verified formalizations of Olympiad-level mathematical competition problems, sourced from [Compfiles](https://github.com/dwrensha/compfiles) and [IMOSLLean4](https://github.com/mortarsanjaya/IMOSLLean4) repository. MathOlympiadBench contains 360 problems, including 158 IMO problems from 1959 to 2024, 131 IMO shortlist problems covering 2006 to 2023, 68 regional mathematical Olympiad problems, and 3 additional mathematical puzzles. 

This model is being released to aid other open-source projects, including those geared towards the upcoming IMO competition. A full paper with all details will be released in the coming weeks.

## 5. Environment Setup

We follow [DeepSeek-Prover-V1.5](https://github.com/deepseek-ai/DeepSeek-Prover-V1.5), which uses Lean 4 version 4.9 and the corresponding Mathlib. Please refer to the following instructions to set up the environments.

### Requirements

* Supported platform: Linux
* Python 3.10

### Installation

1. **Install Lean 4**

   Follow the instructions on the [Lean 4 installation page](https://leanprover.github.io/lean4/doc/quickstart.html) to set up Lean 4.

2. **Clone the repository**

```sh
git clone --recurse-submodules https://github.com/Goedel-LM/Goedel-Prover-V2.git
cd Goedel-Prover-V2
```

3. **Install required packages**
```sh
conda env create -f goedelv2.yml
```

If you encounter installation error when installing packages (flash-attn), please run the following:

```sh
conda activate goedelv2
pip install torch==2.6.0
conda env update --file goedelv2.yml
```

4. **Build Mathlib4**

```sh
cd mathlib4
lake build
```

5. **Test Lean 4 and mathlib4 installation**

```sh
cd ..
python lean_compiler/repl_scheduler.py
```
If there is any error, reinstall Lean 4 and rebuild mathlib4.

## 6. Quick Start
You can directly use [Huggingface's Transformers](https://github.com/huggingface/transformers) for model inference.

```
from transformers import AutoModelForCausalLM, AutoTokenizer
import torch
torch.manual_seed(30)

model_id = "Goedel-LM/Goedel-Prover-V2-8B"
tokenizer = AutoTokenizer.from_pretrained(model_id)
model = AutoModelForCausalLM.from_pretrained(model_id, device_map="auto", torch_dtype=torch.bfloat16, trust_remote_code=True)


formal_statement = """
import Mathlib
import Aesop

set_option maxHeartbeats 0

open BigOperators Real Nat Topology Rat


theorem square_equation_solution {x y : ℝ} (h : x^2 + y^2 = 2*x - 4*y - 5) : x + y = -1 := by
  sorry
""".strip()

prompt = """
Complete the following Lean 4 code:

```lean4
{}```

Before producing the Lean 4 code to formally prove the given theorem, provide a detailed proof plan outlining the main proof steps and strategies.
The plan should highlight key ideas, intermediate lemmas, and proof structures that will guide the construction of the final formal proof.
""".strip()

chat = [
  {"role": "user", "content": prompt.format(formal_statement)},
]

inputs = tokenizer.apply_chat_template(chat, tokenize=True, add_generation_prompt=True, return_tensors="pt").to(model.device)

import time
start = time.time()
outputs = model.generate(inputs, max_new_tokens=8192)
print(tokenizer.batch_decode(outputs))
print(time.time() - start)
```

## 7. Batch Inference and Self-correction

```sh
bash scripts/pipeline.sh
```


### 8. Citation
```
@misc{lin2025goedelproverv2,
    title={Goedel-Prover-V2: The Strongest Open-Source Theorem Prover to Date},
    author={Yong Lin and Shange Tang and Bohan Lyu and Ziran Yang and Jui-Hui Chung and Haoyu Zhao  and Lai Jiang and Yihan Geng and Jiawei Ge and Jingruo Sun and Jiayun Wu and Jiri Gesi and David Acuna and Kaiyu Yang and Hongzhou Lin  and Yejin Choi and Danqi Chen and Sanjeev Arora and Chi Jin},
    year={2025}
}
```
