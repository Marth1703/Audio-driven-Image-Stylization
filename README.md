# Audio-driven Image Stylization

This project combines audio and images to generate stylized image outputs. An audio clip is mapped to a visual style and applied to an input image using an AdaIN-based image stylization pipeline.

## Example results

The top row shows the original images and the bottom row shows the corresponding audio-driven stylizations.

![Example results](examples/ExampleResultsCropped.png)

## Pipeline

![Audio-driven image stylization pipeline](examples/Pipeline.png)

An input image is encoded with the VGG. In parallel, ImageBind extracts an embedding from the audio, and a mapping network converts it into a style representation. AdaIN combines the image content with this audio-derived style, and the decoder generates the stylized output.

## Dataset creation

- **Images:** Stable Diffusion 1.5 was used to generate 10,000 images.
- **Audio:** A split of the [FSD50K dataset](https://zenodo.org/records/4060432) was used to obtain 10,000 audio clips.

The images and audio clips are paired to train the audio-to-style mapping network.

## Setup

Clone the repository together with its submodules, create a Python environment, and install the ImageBind dependencies:

```bash
git clone --recurse-submodules <repository-url>
cd Audio-driven-Image-Stylization
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
python -m pip install --upgrade pip
python -m pip install -r ImageBind/requirements.txt
python -m pip install -e ImageBind
```

The project expects the pretrained AdaIN and mapper checkpoints in the paths configured by `inference.py` before inference can be run. The main scripts are `dataset_creation.py`, `train_mapper.py`, and `inference.py`.
