# MODFLOW 6 Version of RGTIHM

This repository contains the MODFLOW 6 conversion of the [Rio Grande Transboundary Integrated Hydrologic Model](https://www.usgs.gov/centers/new-mexico-water-science-center/science/rio-grande-transboundary-integrated-hydrologic) (RGTIHM). The original model was developed using MODFLOW-One Water Hydrologic Model (MF-OWHM) by the USGS.

USGS Study: 

## Step 1: Set Up the Project Directory

Before downloading any files, create a working directory:

```sh
mkdir MF6
cd MF6
```

Clone the repository:

```sh
git clone git@github.com:mabdazzam/rgtihm.git
```

or

```sh
git clone https://github.com/mabdazzam/rgtihm.git
```

## Step 2: Download and Extract the MF-OWHM Model

Go to the ScienceBase-Catalog page and download all the files for [RGTIHM MF-OWHM Model](https://www.sciencebase.gov/catalog/item/62a12334d34ec53d27701c32):

The downloaded files include:

- SIR2022-5045Thumbnail.jpg
- ancillary.zip
- bin.zip
- georef.zip
- model.zip
- output.zip
- source.zip
- modelgeoref.txt
- readme.txt

Create a directory for MF-OWHM files and move them:

```sh
mkdir owhm
cd owhm
mv ~/Downloads/{SIR2022-5045Thumbnail.jpg,ancillary.zip,bin.zip,georef.zip,model.zip,output.zip,source.zip,modelgeoref.txt,readme.txt} .
```

Extract all the zipped files:

```sh
for i in *.zip; do unzip "$i"; done
```

## Step 3: Run the Conversion Notebook

Navigate to the MF6 directory and launch Jupyter Lab:

```sh
cd ..
jupyter lab
```

Open and run `rgtihm.ipynb` to convert the MF-OWHM model into MODFLOW 6 format.

## Step 4: Run the Converted MODFLOW 6 Model

Once the model is created, navigate to the model directory:

```sh
cd model
```

Run the model using the MODFLOW 6 executable:

If the `mf6` executable is located in `/usr/local/src/modflow6/bin/`, run:

```sh
~/usr/local/src/modflow6/bin/mf6
```

If `mf6` is installed in the system path, simply run:

```sh
mf6
```

## Step 5: Parallel Simulation (Optional)

To generate submodels for parallel execution, run all cells in `splitting.ipynb`.  
This will create submodels in the `splitmodels/` directory.

Run the submodels in parallel using:

```sh
mpiexec -np 4 ~/usr/local/src/mf6/bin/mf6 -p
```

Replace `4` with the number of submodels.

## Troubleshooting: Indexing Errors in WEL and GHB

Errors in WEL and GHB may occur due to indexing differences between MF-OWHM and MODFLOW 6:

- MODFLOW 6 indexing starts from `xorigin` and `yorigin`.
- MF-OWHM indexing starts from `xul` and `yul`.

This difference can cause wells and GHB points to fall outside the active model area. Adjusting the indexing will resolve the issue.# MODFLOW 6 Version of RGTIHM

This repository contains the MODFLOW 6 conversion of the Rio Grande Transboundary Integrated Hydrologic Model (RGTIHM). The original model was developed using MODFLOW-One Water Hydrologic Model (MF-OWHM) by the USGS.

USGS Study: https://www.usgs.gov/centers/new-mexico-water-science-center/science/rio-grande-transboundary-integrated-hydrologic

## Step 1: Set Up the Project Directory

Before downloading any files, create a working directory:

```sh
mkdir MF6
cd MF6
```

Clone the repository:

```sh
git clone git@github.com:mabdazzam/rgtihm.git
```

or

```sh
git clone https://github.com/mabdazzam/rgtihm.git
```

## Step 2: Download and Extract the MF-OWHM Model

Go to the following ScienceBase page and download all files:

https://www.sciencebase.gov/catalog/item/62a12334d34ec53d27701c32

The downloaded files include:

- SIR2022-5045Thumbnail.jpg
- ancillary.zip
- bin.zip
- georef.zip
- model.zip
- output.zip
- source.zip
- modelgeoref.txt
- readme.txt

Create a directory for MF-OWHM files and move them:

```sh
mkdir owhm
cd owhm
mv ~/Downloads/{SIR2022-5045Thumbnail.jpg,ancillary.zip,bin.zip,georef.zip,model.zip,output.zip,source.zip,modelgeoref.txt,readme.txt} .
```

Extract all the zipped files:

```sh
for i in *.zip; do unzip "$i"; done
```

## Step 3: Run the Conversion Notebook

Navigate to the MF6 directory and launch Jupyter Lab:

```sh
cd ~/projects/nmhydro/MF6
jupyter lab
```

Open and run `rgtihm.ipynb` to convert the MF-OWHM model into MODFLOW 6 format.

## Step 4: Run the Converted MODFLOW 6 Model

Once the model is created, navigate to the model directory:

```sh
cd model
```

Run the model using the MODFLOW 6 executable:

If the `mf6` executable is located in `/usr/local/src/modflow6/bin/`, run:

```sh
~/usr/local/src/modflow6/bin/mf6
```

If `mf6` is installed in the system path, simply run:

```sh
mf6
```

## Step 5: Parallel Simulation (Optional)

To generate submodels for parallel execution, run all cells in `splitting.ipynb`.  
This will create submodels in the `splitmodels/` directory.

Run the submodels in parallel using:

```sh
mpiexec -np 4 ~/usr/local/src/mf6/bin/mf6 -p
```

Replace `4` with the number of submodels.

This difference can cause wells and GHB points to fall outside the active model area. Adjusting the indexing will resolve the issue.
