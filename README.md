# 🎨 Neural Style Transfer (AdaIN)

A real-time artistic style transfer web app built with **PyTorch** and **Flask**, using **Adaptive Instance Normalization (AdaIN)** to blend the content of one image with the artistic style of another.

---

## How It Works

The model uses a pre-trained VGG encoder to extract features from both the content and style images. AdaIN aligns the mean and variance of the content features to match those of the style, and a lightweight decoder reconstructs the stylized image — all in a single forward pass.

---

## Project Structure

```
├── app.py          # Flask web application
├── train.py        # Training script
├── utils/
│   ├── models.py   # VGGEncoder and Decoder architectures
│   └── utils.py    # AdaIN, dataset, and transform utilities
├── static/uploads/ # Uploaded and generated images
└── vgg_normalised.pth
```

---

## Setup

```bash
pip install -r requirements.txt
```

Place your pre-trained weights (`vgg_normalised.pth` and `decoder_final.pth`) in the project root, then update the decoder path in `app.py`.

---

## Run the App

```bash
python app.py
```

Visit `http://localhost:5000`, upload a content image and a style image, adjust the **alpha** blending factor (0–1), and hit **Transfer Style**.

---

## Training

```bash
python train.py \
  --content_dir /path/to/content \
  --style_dir /path/to/style \
  --vgg /path/to/vgg_normalised.pth \
  --epochs 10 \
  --style_weight 5 \
  --batch_size 4
```

Checkpoints and sample outputs are saved to `experiment/<name>/`.

---

## Key Parameters

| Parameter | Default | Description |
|---|---|---|
| `alpha` | `1.0` | Style strength (0 = content only, 1 = full style) |
| `style_weight` | `5.0` | Style loss weight during training |
| `content_weight` | `1.0` | Content loss weight during training |
| `lr` | `1e-4` | Learning rate |

---

## References

- [Arbitrary Style Transfer in Real-time with Adaptive Instance Normalization](https://arxiv.org/abs/1703.06868) — Huang & Belongie, 2017