<p align="center">
  <img src="img/codegen_logo_3.png" width="25%" height="25%">
</p>

# CodeGen
This repo includes an official code release for the **CodeGen** models, as presented in the paper, [A Conversational Paradigm for Program Synthesis](https://arxiv.org/abs/2203.13474), by Erik Nijkamp*, Bo Pang*, Hiroaki Hayashi*, Lifu Tu, Huan Wang, Yingbo Zhou, Silvio Savarese, and Caiming Xiong (* indicates equal contribution).

The current version releases the sampling code, while the detailed training code will be released soon.


## Setup
```
git clone https://github.com/salesforce/CodeGen
cd CodeGen

wget -P checkpoints https://storage.googleapis.com/sfr-codegen-research/checkpoints/codegen-350M-mono.tar.gz && tar -xvf checkpoints/codegen-350M-mono.tar.gz -C checkpoints/
wget -P checkpoints https://storage.googleapis.com/sfr-codegen-research/checkpoints/codegen-2B-mono.tar.gz && tar -xvf checkpoints/codegen-2B-mono.tar.gz -C checkpoints/
wget -P checkpoints https://storage.googleapis.com/sfr-codegen-research/checkpoints/codegen-6B-mono.tar.gz && tar -xvf checkpoints/codegen-6B-mono.tar.gz -C checkpoints/
wget -P checkpoints https://storage.googleapis.com/sfr-codegen-research/checkpoints/codegen-16B-mono.tar.gz && tar -xvf checkpoints/codegen-16B-mono.tar.gz -C checkpoints/

python3.8 -m venv .venv
source .venv/bin/activate
pip3 install --upgrade pip setuptools
pip3 install -r requirements.txt
python3 -m jaxformer.hf.sample --model codegen-350M-mono --context "def hello_world():"
```


## Released Models
We release models of various sizes trained on various datasets. The models are named in the following format:
```
codegen-{model-size}-{data}
```

`model-size` has 4 options `350M`, `2B`, `6B`, `16B`.

`data` has 3 options `nl`, `multi`, `mono`. `nl` models are randomly initialized and trained on [the Pile](https://github.com/EleutherAI/the-pile), a 825.18 GB English text corpous. `multi` models are initialized from `nl` models and then trained on a corpus with code data of multiple programming languages. `mono` models are initialized from `multi` models and then trained on a corpus with Python code.

The model names can be provided to the `--model` flag for `sample.py`. See a sample usage above in Setup.


## Citation
If you find our code or paper useful, please cite the paper:
```
@article{Nijkamp2022ACP,
  title={A Conversational Paradigm for Program Synthesis},
  author={Nijkamp, Erik and Pang, Bo and Hayashi, Hiroaki and Tu, Lifu and Wang, Huan and Zhou, Yingbo and Savarese, Silvio and Xiong, Caiming},
  journal={arXiv preprint},
  year={2022}
}
```


## License
Our code is BSD-3 licensed. See LICENSE.txt for details.
