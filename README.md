# 🤖 Face Recognition — Computer Vision

A Python computer vision toolkit built on the [`face_recognition`](https://github.com/ageitgey/face_recognition) library (powered by dlib). Provides four focused scripts covering the core face recognition pipeline: detection, extraction, matching, and annotated identification.

---

## ✨ Features

| Script | What it does |
|---|---|
| `findfaces.py` | Detects and counts faces in a group photo |
| `pullfaces.py` | Extracts and saves each detected face as an individual image |
| `facematch.py` | Compares an unknown face against a known reference and prints a match result |
| `indentify.py` | Identifies multiple known faces in a group photo and draws labelled bounding boxes |

---

## 📁 Project Structure

```
face-recognition-computer-vision/
├── img/
│   ├── known/          # Reference images (e.g. Bill Gates.jpg, Steve Jobs.jpg, Elon Musk.jpg)
│   ├── unknown/        # Images to test matching against (e.g. d-trump.jpg)
│   └── groups/         # Group photos for detection & identification
├── findfaces.py        # Count faces in a group image
├── pullfaces.py        # Extract & save individual face crops
├── facematch.py        # Binary face comparison (known vs unknown)
├── indentify.py        # Multi-face identification with bounding box overlay
├── Pipfile             # Pipenv dependency manifest
└── Pipfile.lock        # Locked dependency versions
```

---

## 🛠 Requirements

- Python 3.7+
- `face_recognition` — wraps dlib's face detection and 128-d encoding models
- `Pillow` — used for image drawing and saving in `pullfaces.py` and `indentify.py`
- `autopep8` (dev) — code formatting

> **Note:** `face_recognition` requires **dlib** which in turn requires **CMake** and a C++ compiler. On most systems you'll need to install these before running `pip install face_recognition`. See [dlib installation notes](http://dlib.net/compile.html) if you hit build errors.

---

## 🚀 Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/richardy-lobo-sapan/face-recognition-computer-vision.git
cd face-recognition-computer-vision
```

### 2. Install dependencies

Using **Pipenv** (recommended):

```bash
pip install pipenv
pipenv install
pipenv shell
```

Or using **pip** directly:

```bash
pip install face_recognition Pillow
```

### 3. Add your images

Place your reference images in `img/known/`, unknown images in `img/unknown/`, and group photos in `img/groups/`. Update the filenames in each script to match.

---

## 📋 Usage

### Count faces in a group photo

```bash
python findfaces.py
# → There are 4 people in this image
```

### Extract and save individual face crops

```bash
python pullfaces.py
# Saves each detected face as a separate .jpg (named by its top-coordinate)
```

### Compare one face against a known reference

```bash
python facematch.py
# → This is Bill Gates  /  This is NOT Bill Gates
```

### Identify multiple people in a group photo

```bash
python indentify.py
# Opens annotated image and saves it as identify.jpg
```

---

## 🧠 How It Works

All scripts rely on the same underlying pipeline:

1. **Load** — read the image file into memory with `face_recognition.load_image_file()`
2. **Locate** — find bounding box coordinates for every face via `face_locations()`
3. **Encode** — compute a 128-dimensional face embedding for each detected face via `face_encodings()`
4. **Compare** — measure Euclidean distance between encodings using `compare_faces()` (or `face_distance()` for a numeric score)
5. **Annotate** — use Pillow's `ImageDraw` to overlay bounding boxes and name labels, then save the result

---

## 🖼 Image Directory Guide

```
img/
├── known/
│   ├── Bill Gates.jpg
│   ├── Steve Jobs.jpg
│   └── Elon Musk.jpg
├── unknown/
│   └── d-trump.jpg
└── groups/
    ├── team1.jpg          ← used by pullfaces.py
    ├── team2.jpg          ← used by findfaces.py
    └── bill-steve-elon.jpg ← used by indentify.py
```

> Images are not included in the repository. You'll need to supply your own photos matching the paths above, or update the paths in each script.

---

## 📦 Dependencies

```toml
[packages]
face-recognition = "*"

[dev-packages]
autopep8 = "*"

[requires]
python_version = "3.7"
```

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is open source. The `face_recognition` library is licensed under the MIT License.

---

*Built with [face_recognition](https://github.com/ageitgey/face_recognition) by Adam Geitgey · [dlib](http://dlib.net/) by Davis King*
