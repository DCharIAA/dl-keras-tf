Installing Requirements
================

This notebook will help you install all the required packages and data
sets used throughout this workshop.

# Packages

Although this training focuses on the **keras** package, we will use
several additional packages throughout our modules. At the beginning of
each module I state the primary purpose of the packages used so if some
of these packages are not familiar, that is okay.

Run the following code chunk to install packages not already installed.
Within the RStudio workshop, this has already been taken care of for
you.

``` r
pkgs <- c(
  "AmesHousing",
  "caret",
  "crayon",
  "data.table",
  "fs",
  "glue",
  "here",
  "jpeg",
  "keras",
  "plotly",
  "recipes",
  "ROCR",
  "Rtsne",
  "rsample",
  "testthat",
  "text2vec",
  "tidyverse"
)


missing_pkgs <- pkgs[!(pkgs %in% installed.packages()[, "Package"])]

if (length(missing_pkgs) > 0) {
  install.packages(missing_pkgs)
}
```

Depending on how often you update your packages you may also want to see
if any of these packages that you had installed previously need to be
updated to more recent versions. You can run the following to make
necessary
updates.

``` r
update.packages(oldPkgs = pkgs, ask = FALSE, repos = "https://cran.rstudio.com/")
```

# Datasets

We will use a variety of datasets throughout this workshop; many of
which are too large to hold within the github repository. The following
will help you download all necessary datasets and store them in the
`\data` folder. For those attending the RStudio workshop, this has
already been taken care of for you.

``` r
data_directory <- here::here("materials", "data")

if (!dir.exists(data_directory)) {
  dir.create(data_directory)
}
```

## Yelp reviews

Used for sentiment classification. Contains 1,569,264 samples from the
[Yelp Dataset Challenge 2015](https://www.yelp.com/dataset/challenge).
This subset has 280,000 training samples and 19,000 test samples in each
polarity.

``` r
yelp_data <- file.path(data_directory, "yelp_review_polarity_csv")
if (!dir.exists(yelp_data)) {
  url <- "http://s3.amazonaws.com/fast-ai-nlp/yelp_review_polarity_csv.tgz"
  download.file(url, destfile = "materials/data/tmp.tar.gz")
  untar("materials/data/tmp.tar.gz", exdir = "materials/data/")
  invisible(file.remove("materials/data/tmp.tar.gz"))
}
```