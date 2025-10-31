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

Dataset/                     
  BroadReactive/...
  StrictReactive/...

PredictionDataset/           # ACTIVE dataset for prediction
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



2. Installing Requirements (💡 **Note:** You can either use the pre-supplied `requirements.txt` to install all dependencies at once, **or** follow the manual steps in `INSTALLATION.md` to create a new conda environment and install Jupyter Notebook and all required packages.)


3. Open `TrainSegmentationModel.ipynb` and set:
   ```python
   BATCH_SIZE = 1
   DEFAULT_LEARNING_RATE = 0.0001
   NUM_EPOCHS = 200
   model_list = ["UnetPlusPlus"]
   backbone_list = ["vgg19"]
   ```
4. Run all cells; the trained model will be saved under `Models/` by default. (Pay attention if you train a model with the exact same Network and Backbone of the pre-trained model, it will be overwritten)

