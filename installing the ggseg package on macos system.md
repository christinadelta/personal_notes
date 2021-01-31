## Install the ggseg and ggseg3d R packages on macOs Mojave 


I recently heard about the  **ggseg** and **ggseg3d** packages for visualizing brain/fMRI statistics on several atlasses with R and thought to install it and give it a go! To be entirely honest I was a bit skeptic in the beginning, R is a **GREAT & POWERFULL** tool for statistical analysis, but for visualizing brain data..? hhhmmm. 

Nevertheless, I thought to try it and it took me sometime to sucessfully install the package, but now that I managed to do it, and work around a bit, I find it quite awsome!! 

I work with macOS mojave and installing **ggseg** was painfull! Here are my steps from A-Z:

### STEP 1. Open Rstudio and install the ggseg package

You won't find the package through the oficial CRAN page or using the **install R packages** option of Rstudio. The easiest way is installing it through [github] (https://github.com/LCBC-UiO/ggseg). So, following the steps provided by the developers of the package, in Rstudio console type:

```
install.packages("remotes")
remotes::install_github("LCBC-UiO/ggseg", build_vignettes = TRUE)
```

If it works then you are probably good to go! But unfortunatelly it didn't work for me. A message appeared on the console asking me to update a few needed packages before installing **ggseg**, and one of them is called **sf**. Briefly, the sf package is used as a standardized way to encode spatial vector data, but more info can be found [here](https://cran.r-project.org/web/packages/sf/index.html). For reasons that I don't fully understand, I couldn't install the sf package using the traditional way (click on install r packages, find the sf package, etc...). So, I googled the problem (a lot!) and by combining 2-3 different sources, managed to find a working solution. 

So, if you can't install the sf package go to step 2.

### STEP 2. Install a couple system-related packages before going back to Rstudio

These steps worked for me..

**Step 2.1** Install or update Homebrew 

To install homebrew:

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```

If you already have brew, you need to update it before using it:

```
brew update
```
**Step 2.2** Next, isntall the following packages:

```
brew install pkg-config
brew install gdal proj geos
```
If that works, skip the next step (step 2.2.1), if it doesn't work:

**Step 2.2.1** make a file writeable for homebrew. 

If step 2.2 yelds some error like this:

```
You should change the ownership of these directories to your user.
sudo chown -R $(whoami) /usr/local/share/man/man5

And make sure that your user has write permission.
chmod u+w /usr/local/share/man/man5
```

 that's probably because you need to make the above file writable for homebrew:
 
 ```
 sudo chgrp -R admin /usr/local
 sudo chmod -R g+w /usr/local 
 ```
 Then run again **step 2.2**.
 
 **Step 2.3** I am not entirely sure if this step is necessary, but I included this on my terminal:
 
 ```
 export LDFLAGS="-L/usr/local/opt/libpq/lib"
 export CPPFLAGS="-I/usr/local/opt/libpq/include"
 ```
 

### STEP 3. Try to install the sf package again.
 
After installing the system-related stuff, re-open Rstudio and type the commands:
 
 ```
 install.packages("rgeos", repos="http://R-Forge.R-project.org", type="source")
 install.packages("rgdal", repos="http://R-Forge.R-project.org", type="source")
 library(devtools)
 install_github("r-spatial/sf", configure.args = "--with-proj-lib=/usr/local/lib/")
 ```


### STEP 4. Re-try to install the ggseg package  

After installing sf, restart Rstudio and try to install **ggseg** again:

```
install.packages("remotes")
remotes::install_github("LCBC-UiO/ggseg", build_vignettes = TRUE)
```
If it works, the great! But again, it didn't work for me. This time the error looked like this:

```
SUMMARY: processing the following file failed:     ‘freesurfer_files.Rmd’      Error: Vignette re-building failed.   Execution haltedError: Failed to install 'ggseg' from GitHub:  System command 'R' failed, exit status: 1, stdout + stderr (last 10 lines):E> --- finished re-building ‘geom-sf.Rmd’E> E> --- re-building ‘ggseg.Rmd’ using rmarkdownE> --- finished re-building ‘ggseg.Rmd’E> E> SUMMARY: processing the following file failed:E>   ‘freesurfer_files.Rmd’E> E> Error: Vignette re-building failed.E> Execution halted
```
After googling it, I found a **temporary** but working solution provided by the developers [here](https://github.com/LCBC-UiO/ggseg/issues/30). So, the problem starts with the *failed vignette re-building* , and the developers suggest changing the option of building the vignette to **FALSE**:

```
remotes::install_github("LCBC-UiO/ggseg, build_vignettes = F)
```
And that's it! For now it's working :) 














