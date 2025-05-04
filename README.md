# Land Surface Temperature estimation using satellite images and meteorological data

## Overview
Land Surface Temperature (LST) is an important indicator urban planners use to mitigate the negative effects of urban heat islands. Unfortunately, high resolution LST maps are available once every 16 days only. This project provides deep learning models for obtaining high accuracy LST estimates on days where satellite images are not available. We leverage our knowledge of the physics behind heat transfer to improve model performance.

---

## Project Hierarchy
```
├── Models/             # Model implementations
├── Preprocessing/             # Jupyter notebook for data prep
├── Testing/                   # Test scripts & evaluation notebooks
├── Semantic Segmentation/                   # Image segmentation related to failed attempt
└── README.md                  # This file
```

---

## Quick Start
1. Download the necessary datasets from Landsat 8 and NOAA (see Preprocessing for details).
2. Open the `Preprocessing.ipynb` notebook in Google Colab.
3. Mount your Google Drive containing Landsat 8 and NOAA files.
4. Update the relevant path variables in the first cell.
5. Run all cells in the notebook to preprocess the data for training
6. Select a model from the `Models/` directory and run all cells to train from scratch.

---

## Preprocessing
**Setup Instructions:**
1. **Download Official Landsat 8 Data**
   - From USGS or Google Earth, download the NDVI, NDBI, and NDWI bands.
   - Choose New York City if you want to replicate our results, but we encourage you to try our models on different cities.
2. **Download Hourly Meteorological Data**
   - For New York City CSVs, download from NOAA Global Hourly: https://www.ncei.noaa.gov/access/search/data-search/global-hourly
   - If evaluating on another city, look for similar data or compile your own CSV file.
3. **Update Preprocessing Paths**
   - In the first cell of Preprocessing.ipynb, set LST_PATH to your Landsat folder and METEO_CSV_PATH to the NOAA CSV location.

Once paths are set, run the notebook cells to generate 64×64 patches and clean the data.

---

## Datasets
- **Cleaned Meteorological Data:** [Google Drive File](https://drive.google.com/file/d/1ss4D_ZkzQWdW9VIsAOJFZBPHo05u04sR/view?usp=drive_link)
- **Final cleaned LST with Meteo:** [Google Drive Folder](https://drive.google.com/drive/folders/1nXb8mzun6akRigNKNxWN9S0lplsE6m3V?usp=drive_link)

---

## Models
- **Vit+MLP**: Vision Transformer baseline model, enhanced through hyperparameter tuning and selective unfreezing of the final layer.
- **ViT+LSTM**: Vision Transformer backbone fused with a 6-hour LSTM head to incorporate sequential meteorological inputs.
- **VIT+PINN+MLP**: Physics-informed Vision Transformer integrating Newtonian cooling priors to enforce physically realistic temperature decay patterns. Best out of the 3 models


---

## Testing
We trained our models on data from 2018 to 2022 and evaluated our implementations using held-out LST and meteorological records from **2023**.

To run tests:
1. Mount your Google Drive in Colab or ensure local access to your data directories.
2. Update the path variables in the first cell of each testing notebook to point to your LST and meteo data.
3. Execute the notebook cells or run the test scripts directly in Colab or locally.

---

## Results
ALl models achieved very reasonable results (RMSE < 0.35 °C). Our best model was the Physics-informed ViT, achieving and RMSE of **0.21 °C**.

---

## Authors
- Ahmad Hlayhel (@ahmadhlayhel)
- Boulos Boulos (@PabloBoulos)
- Charbel Hannoun (@channoun)

---

## License
This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
