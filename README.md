# Astrocyte Segmentation (UNet++ / VGG19)

Two Jupyter notebooks:
- `TrainSegmentationModel.ipynb` — train your own model (any image size).
- `AutomaticSegmentation.ipynb` — run the pretrained model.

## Folder structure
```text
Models/
  unetplusplus_vgg19/
    net.pth                 # put the pretrained weights here

Images/                      # ACTIVE dataset for training
  Train/
    Raw/
    Labels/
  Test/
    Raw/
    Labels/

Dataset/                     # optional: storage for multiple datasets
  BroadReactive/...
  StrictReactive/...

PredictionDataset/           # ACTIVE dataset for inference/prediction
  <AnyFolderName>/
    Raw/                     # place raw images here
    Segmentation/            # binary outputs will be written here

TrainSegmentationModel.ipynb
AutomaticSegmentation.ipynb
requirements.txt
INSTALLATION.md
README.md
```

### About the `Dataset/` folder
- Existing datasets (`BroadReactive`, `StrictReactive`).
- **Pretrained weights provenance:** the provided **UNet++/VGG19** weights (`net.pth`) were **trained on the `StrictReactive` dataset** (strongly reactive labels only).
- When you want to **train**, copy the desired dataset into `Images/` with the exact layout above.

### Masks / labels
- **Binary segmentation** (astrocyte vs background).
- Masks must be **0/1**.
- Filenames must match between `Raw/` and `Labels/` (same width/height).
- 
### How to run inference (pretrained UNet++/VGG19)
1. Prepare an input set under **PredictionDataset** (the set folder can be named anything):
   ```text
   PredictionDataset/MySet/Raw/           # put images here
   PredictionDataset/MySet/Segmentation/  # will be created automatically; outputs saved here
   ```
2. Ensure inputs are `631×486` for this pretrained model (resize/pad in the notebook if needed).
3. Open `AutomaticSegmentation.ipynb` and set:
   ```python
   model = "UnetPlusPlus"
   backbone = "vgg19"
   ```
4. Run all cells. Binary masks (0/1) will be saved in `Segmentation/` with matching filenames.

### How to train your own model
1. Put your chosen dataset under `Images/` in the same structure.



2. Installing Requirements (💡 **Note:** You can either use the pre-supplied `requirements.txt` to install all dependencies at once, **or** follow the manual steps below to create a new conda environment and install Jupyter Notebook and all required packages.)

   ### Instructions for installing the packages
   #### 1. Create and activate a new environment
   Open **Anaconda Prompt** and run:
   ```bash
   conda create --name PathologySegmentation python=3.8
   conda activate PathologySegmentation
   ```


   #### 2. Install Jupyter Notebook
   ```bash
   conda install jupyter
   ```

   #### 3. Install pip
   ```bash
   conda install pip
   ```

   #### 4. Install the required packages
   You can install the packages manually as follows:
   ```bash
   # Core libraries
   conda install -c conda-forge opencv
   conda install pandas
   conda install matplotlib
   conda install pillow
   conda install numpy

   # PyTorch
   # CPU version:
   conda install pytorch torchvision cpuonly -c pytorch
   # GPU version (CUDA 11.8):
   pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118

   # Additional packages
   pip install split-folders
   pip install scikit-learn
   pip install torchsummary
   pip install segmentation_models_pytorch
   pip install torchinfo
   ```

   #### 5. Launch Jupyter Notebook
   Once all packages are installed, launch Jupyter Notebook from the same environment:
   ```bash
   jupyter notebook
   ```

   ---

   **Alternative (one step):**
   If you prefer a single-step installation, from within the activated environment run:
   ```bash
   pip install -r requirements.txt
   ```

3. Open `TrainSegmentationModel.ipynb` and set:
   ```python
   BATCH_SIZE = 1
   DEFAULT_LEARNING_RATE = 0.0001
   NUM_EPOCHS = 200
   model_list = ["UnetPlusPlus"]
   backbone_list = ["vgg19"]
   ```
4. Run all cells; checkpoints will be saved under `Models/` by default.

