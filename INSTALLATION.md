# 🔧 Environment Setup & Installation Guide

This project requires Python 3.8 and a set of scientific and deep learning libraries.  
Follow the steps below to create and configure the environment.

---

## 1. Create the Conda Environment

Open **Anaconda Prompt** and run:

```bash
conda create --name AstrocyteSegmentation python=3.8
```

Activate the environment:

```bash
conda activate AstrocyteSegmentation
```

To exit the environment:

```bash
conda deactivate
```

---

## 2. Install Jupyter and pip

```bash
conda install jupyter
conda install pip
```

---

## 3. Install Required Packages

### Core Scientific Libraries
```bash
conda install numpy
conda install pandas
conda install matplotlib
conda install pillow
conda install -c conda-forge opencv
```

### Machine Learning / Deep Learning
#### Option A — CPU only
```bash
conda install pytorch torchvision cpuonly -c pytorch
```

#### Option B — GPU (CUDA 11.8, NVIDIA required)
```bash
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118
```

---

## 4. Additional Python Libraries

```bash
pip install split-folders
pip install scikit-learn
pip install torchsummary
pip install torchinfo
pip install segmentation-models-pytorch
pip install thop
```

---

## 5. Verify Installation

Check Python and Torch:

```bash
python -c "import torch; print(torch.__version__); print('CUDA available:', torch.cuda.is_available())"
```

---

## 6. Launch Jupyter Notebook

From the same environment:

```bash
jupyter notebook
```

Then open `TrainSegmentationModel.ipynb` and follow the instructions inside (set `epochs`, `Network`, and `Backbone`).

---

✅ That’s it. You now have the **AstrocyteSegmentation** environment ready for training and using your astrocyte segmentation model.
