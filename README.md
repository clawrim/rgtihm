## MDOFLOW 6 version of RGTIHM
This repo is about the conversion of Rio Grande Transboundary Integrated Hydrologic Model (RGTIHM), a MODFLOW-One Water Hydrologic Model study by the USGS into MODFLOW 6.
USGS Study: https://www.usgs.gov/centers/new-mexico-water-science-center/science/rio-grande-transboundary-integrated-hydrologic

# Step 1: Create a dir before downloading anything
`mkdir MF6'
`cd MF6`

clone the repo
`git@github.com:mabdazzam/rgtihm.git`

or 

`git clone https://github.com/mabdazzam/rgtihm.git``

# Step 2 Download RGTIHM Mf-OWHM model

https://www.sciencebase.gov/catalog/item/62a12334d34ec53d27701c32 go to this url, click on the download all button and download all the files (also listed blow);
- SIR2022-5045Thumbnail.jpg
- ancillary.zip
- bin.zip
- georef.zip
- model.zip
- output.zip
- source.zip
- modelgeoref.txt
- readme.txt

`mkdir owhm`
`cd owhm`

move the owhm files to current directory
`mv ~/Downloads/{SIR2022-5045Thumbnail.jpg,ancillary.zip,bin.zip,georef.zip,model.zip,output.zip,source.zip,modelgeoref.txt,readme.txt} .`

unzip all the zipped directories
`for i in *.zip; do unzip "$i"; done

Now you can run jupyter lab from your source dirctory "MF6" and run the 'rgtihm.ipynb' to translate the RGTIHM MF-OWHM into MODLFOW6 model.

Once the model is created, run the model using the mf6 executable

`cd model`
`~path/to/mf6` for example `~/usr/local/src/modflow6/bin/mf6`

Or if you have modflow6 executables copied into the bin, simply run;
`mf6`

## Parallel Simulation
Run all the cells from the splitting.ipynb, it will create the sub models in splitmodels/ directory. 

To execute the submodels in parallel,
run `mpiexec -np 4{n_submodels} ~/usr/local/src/mf6/bin/mf6 -p`


The error in wel and ghb is because of the indexing. mf6 indexing start from xorigin and yorigin whereas the indexing in the mf-owhm Frmwk_cells starts from xul and yul, causing the wels and ghb to go outside the active area. 
