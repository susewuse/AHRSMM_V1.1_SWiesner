# AHRSMM_V1.1

Adaptive High-Resolution Soil Moisture Map (AHRSMM) Version 1.1

To map daily surface (0-5 cm) and rootzone (0-1 m) soil moisture at any location in the continental USA, with any spatial resolution (e.g., 30 m to 1 km) and on any date since 2016/01/01, please do the following:

Please download all the 23 zip files and unzip them into one folder. Before you run the following R code, make sure you have the latest version of RTools (https://cran.r-project.org/bin/windows/Rtools/) and miniconda (https://docs.conda.io/en/latest/miniconda.html) installed.

1) Fitting Machine Learning Models. 
Open the "AHRSMM_V1.1.R" file to start the model fitting. Alternatively, load the ".RData" which contains the fitted machine learning models and downloaded covariates for the sample Wisconsin field. You can also choose to fit the models yourself but it may take a longer time.

2) Set up the Google Earth Engine.
If you have trouble using "ee_Initialize(...)", please set your Python environment manually from here: https://github.com/r-spatial/rgee/tree/help/rstudio/. Details: 1. Follow Step 1 to install earthengine-api using conda (this step can be skipped if you have no problem running ee_install(). 2. In R Studio, Go to Tools > Global Options > Python, set the Python interpreter to the directory where you have rgee: ...\r-miniconda\envs\rgee\python.exe 3. Terminate your R session and run ee_Initialize(email = 'jhuang426@wisc.edu', drive = TRUE) with your email address replaced the default one. Note: You should register Google Earth Engine Account using your email address first. If the initialization with "email" does not work, please replace the argument "email" with "user" and run this: ee_Initialize(user = 'jhuang426@wisc.edu', drive = TRUE) or run the line without "email" or "user" ee_Initialize(drive = TRUE). When a web browser pops up and asks you to allow Google Earth Engine/R to access your Google Account, please select "Yes" to all the checkboxes (even the hidden boxes). 

3) Download remote sensing data for target study areas. 
Generate a shapefile for the study field (region of interest, ROI) and load it to the R environment. Define the spatial resolution and the starting and ending dates you want to generate a surface soil moisture map.
Download the covariates from the Google Earth Engine and Google Cloud Storage using the R code. You need to create a Google Earth Engine account and initialize it using the R code.

4) Generate soil moisture maps using existing models.
Run the fitted machine learning model (now a Random Forest model, can be changed to others using the "caret:train" function) and predict soil moisture onto the region of interest defined by the shapefile.

5) Refit models using new soil moisture data (adative machine learning) and regenerate soil moisture maps.
If you have in situ soil moisture probe data, prepare them in a .csv file format using the template "Huges_VWC.csv". Then load your in situ measurements to the R environment and refit the model using the R codes. After that, apply the updated model to the ROI and generate the new soil moisture map. This is the "Adaptive" feature of the High-Resolution Soil Moisture Map. After you include local in situ data, the model will have an improved performacne at your own fields. Note: your input data is only accesible by yourself and will not be available to others.

If you have trouble using the R code or if you are interested in the collaboration on further improving this model, please feel free to send an email to Jingyi Huang (jhuang426@wisc.edu).

