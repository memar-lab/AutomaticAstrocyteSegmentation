# Astrocyte Segmentation (UNet++ / VGG19)

Two Jupyter notebooks:
- `TrainSegmentationModel.ipynb` — train your own model (any image size).
- `AutomaticSegmentation.ipynb` — run the pretrained model.

**Pretrained model input size:** `631 × 486` (W × H). For inference, resize or pad images to this size.  
Training accepts **any** consistent input size.

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
2. Open `TrainSegmentationModel.ipynb` and and set:
   ```python
   BATCH_SIZE = 1
   DEFAULT_LEARNING_RATE = 0.0001
   NUM_EPOCHS = 200
   model_list = ["UnetPlusPlus"]
   backbone_list = ["vgg19"]"
   ```
3. Run all cells; checkpoints will be saved under `Models/` by default.

### About the `Dataset/` folder
- Existing datasets (`BroadReactive`, `StrictReactive`).
- **Pretrained weights provenance:** the provided **UNet++/VGG19** weights (`net.pth`) were **trained on the `StrictReactive` dataset** (strongly reactive labels only).
- When you want to **train**, copy the desired dataset into `Images/` with the exact layout above.

### Masks / labels
- **Binary segmentation** (astrocyte vs background).
- Masks must be **0/1**.
- Filenames must match between `Raw/` and `Labels/` (same width/height).
