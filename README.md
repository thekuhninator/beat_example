# beat_example
An example of how to run the R package BEAT. Comes with example data and an example R notebook. Below is the R notebook that is provided in this GitHub repository. Clone the repo to run it yourself.

Let's start by installing BEAT.

```{r}
# if you do not yet have devtools install devtools
install.packages("devtools")

# load the devtools library and install BEAT
library(devtools)
install_github('thekuhninator/beat')
library(beat)
```

Now let's try running BEAT on the uncorrect dataset...

```{r}
input_counts <- "./example_data/dataset1/dataset1_gene_counts.csv"
input_annot  <- "./example_data/dataset1/dataset1_metadata.csv"
output_dir <- "./beat_output/dataset1_uncorrected"
dataset_name <- "dataset1_uncorrected"
original <- TRUE
beat::beat(input_counts, input_annot, output_dir, dataset_name, original)
```

Great. Now let's try running beat on the limma corrected example dataset...

```{r}
input_counts <- "./example_data/dataset1_limma/dataset1_limma_gene_counts.csv"
input_annot  <- "./example_data/dataset1_limma/dataset1_limma_metadata.csv"
output_dir <- "./beat_output/dataset1_limma"
dataset_name <- "dataset1_limma"
original <- FALSE
beat::beat(input_counts, input_annot, output_dir, dataset_name, original)
```

Now we have produced two beat files... we can open the html reports and examine them.

We can also combine them using the mutlibeat tool to compare the severity of the batch effect in the two datasets.

```{r}
parent_dir <- "./example_output"
output_dir <- "beat_output/multi_beat_output"
output_name <- "dataset_1"
beat::multi_beat(parent_dir, output_dir, output_name)
```

Note how multibeat will recursively check the parent_dir given and find all beat files. This concludes the tutorial. Please look at what is outputed from running this script and the example output to see if everything worked correctly. I hope BEAT is helpful for you and your project.
