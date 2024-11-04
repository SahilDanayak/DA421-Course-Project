# DA421 Course Project
## Multi-modal Sarcasm Detection

# Table of Contents

- [Abstract](#abstract)
- [Installation](#installation)
- [Installing Dependencies](#installing-dependencies)
- [Dataset Preprocessing](#dataset-preprocessing)
- [Execution](#execution)
- [Acknowledgements](#acknowledgements)

## Abstract

Detecting sarcasm in social media posts, often expressed with a mix of text and images, presents unique challenges in sentiment analysis and intent recognition. Many current multi-modal sarcasm detection methods struggle to accurately interpret the subtle cues arising from text-image interactions, often leading to inflated performance claims. In this project, we leverage the [CLIP (Contrastive Language-Image Pre-Training)](https://arxiv.org/abs/2103.00020v1) model, which integrates cross-modality information within each encoder to enhance the representation of text and images together. We also incorporate a dynamic, fixed-length dual-channel memory to retain historical information on test samples during inference. This memory functions as a non-parametric classifier to improve prediction accuracy, strengthening the robustness of our multi-modal sarcasm detection model.


## Installation

### Setting Up the Virtual Environment

To manage the Python environment, we use [`pyenv`](https://github.com/pyenv). This project was developed using Python 3.9.19, and using this specific version is recommended to avoid potential compatibility or performance issues.

If you haven't installed `Python 3.9.19`, please run the following command:

```bash
pyenv install 3.9.19
```

> Note: pyenv attempts to download and compile the specified Python version, though compilation may fail due to unmet system dependencies or exhibit issues at runtime.
> For any issues refer (https://github.com/pyenv/pyenv/wiki#suggested-build-environment)

Then, create a virtual environment with the following command:

```bash
pyenv virtualenv 3.9.19 mmsd-3.9.19
```

Then, activate the virtual environment with:

```bash
pyenv activate mmsd-3.9.19
```

### Installing Dependencies

Dependencies are managed with [`poetry`](https://python-poetry.org/). Please install Poetry first, then use the command below to install dependencies from the `poetry.lock` file:

```bash
poetry install
```

To start the Poetry shell, use:

```bash
poetry shell
```

## Dataset Preprocessing

We use the [datasets](https://huggingface.co/docs/datasets/en/index) library to load the dataset from HuggingFace.

The code will automatically download the MMSD2.0 dataset from Hugging Face. Ensure an active internet connection is available for the complete download.

[![Dataset on HF](https://huggingface.co/datasets/huggingface/badges/resolve/main/dataset-on-hf-sm.svg)](https://huggingface.co/datasets/coderchen01/MMSD2.0/)

### Adding a Manual Dataset

To add a manual dataset, follow these steps:

We provide a script, [convert_mmsd2_to_imagefolder_data.py](./src/convert_mmsd2_to_imagefolder_data.py), that converts MMSD2.0 into a format compatible with the Hugging Face datasets library and uploads it to Hugging Face. Refer to [MMSD2.0](https://github.com/JoeYing1019/MMSD2.0?tab=readme-ov-file) for data preparation instructions.

After preparing the data, update line 12 in [convert_mmsd2_to_imagefolder_data.py](./src/convert_mmsd2_to_imagefolder_data.py) with the dataset path, and line 64 with the desired dataset name on Hugging Face (you’ll need to log in with `huggingface-cli`—details are available [here](https://huggingface.co/docs/datasets/en/upload_dataset#upload-with-python)).

Run the script with:

```bash
python src/convert_mmsd2_to_imagefolder_data.py
```

Lastly, update line 69 in [dataset.py](./src/dataset.py) to specify the name of the uploaded dataset.

## Execution

Run the following command to reproduce the results:

```shell
./src/run_main_results.sh
```


## Acknowledgements

- [Hugging Face](https://huggingface.co/)
- [CLIP](https://github.com/openai/CLIP)
- [MMSD2.0 Benchmark](https://github.com/JoeYing1019/MMSD2.0?tab=readme-ov-file)