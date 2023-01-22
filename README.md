# WSSTATEC
This repository is dedicated to the project of time series forecast, done in R langauge.
The dataset used for the project is the [Delhi daily climate data](https://www.kaggle.com/datasets/sumanthvrao/daily-climate-time-series-data).
Three modesl are used for forecasting, which are autoregressive–moving-average (ARMA), vector autoregression (VAR), and two neural network models, feedforward and long-short-term-memory.

To view this project, you can look at the [HTML rendering of the Rmardkown file](https://htmlpreview.github.io/?https://raw.githubusercontent.com/berserkhmdvhb/WSSTATEC/main/ts1.html).
However, since the project includes interactive plots, which are not presentable by clicking on the link, I suggest to clone the repository and then open the HTML file, with following command:

```
git clone git@github.com:berserkhmdvhb/WSSTATEC.git
```



# Usage

The libraries required for this project is provided in the `renv.lock` file.

##  Interoperability between Python and R 
For the LSTM model, as R doesn't have native `tensorflow` and `keras` libraries, a python virtual environment is connected to this project so as to use the LSTM model. To connect Rstudio to the virtual environment and incorporate required python libraries in the project, the manner partly explained in website of [Tensorflow for R](https://tensorflow.rstudio.com/install/) is followed. Some steps are missing website, so a comprehensive guideline is provided in the following:

1. Install the tensorflow R package as follows:

```r
install.packages("keras")
```

2. Install [`reticulate` library](https://rstudio.github.io/reticulate/) as follows:

```r
install.packages("reticulate")
```

3. Configure R with a Python installation it can use, like this:

```r
library(reticulate)
path_to_python <- install_python()
virtualenv_create("r-reticulate", python = path_to_python)
```
Note that if you already have Python installed, you don’t need to call `install_python()` and instead can just supply an absolute path to the Python executable.
So far the python virtual environment with the name `r-reticulate` should have been created.

4. Now we intend to install `keras` on the virtual environment.

```r
library(keras)
install_keras(envname = "r-reticulate")
```

5. Although by now the `r-reticulate` virtual environment contains the required python packages, yet the reticulate won't run Python from this environment and instead will load it from its default path defined in the `RETICULATE_PYTHON`. The default path in Linux is `/usr/bin/python3`. To overcome this, we should unset the variable.

```r
Sys.unsetenv("RETICULATE_PYTHON") 
use_virtualenv("~/.virtualenvs/r-reticulate")
```

6. Now if we load the `keras` library, the Python packages are loaded from the virtual evnironment.


