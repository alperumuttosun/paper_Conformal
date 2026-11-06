# R code for conformal prediction sets in stylometric authorship attribution, using the English, French and German collections of the European Literary Text Collection (ELTeC).

## How to run

1. Install R (tested with R 4.5.2). Missing packages are installed automatically: `xml2`, `jsonlite`, `openxlsx`, `readxl`, `ggplot2` and, optionally, `ggrepel`.
2. Open `paper_conformal_step01-10.R` and set `base_dir` near the top of the script to a folder on your computer. All outputs are written to a `paper_conformal` subfolder of it.
3. Run the whole script. Each step is skipped if its output already exists, and the corpora are downloaded only once. Some steps take several hours.

## Steps

| Step | What it does |
|---|---|
| 01 | Downloads the English ELTeC collection from GitHub and extracts the text of each novel. |
| 02 | Splits novels into chunks, computes Cosine Delta distances on the most frequent words and builds conformal candidate-author sets (English only). |
| 03 | Adds cluster-bootstrap intervals, the hierarchical conformal procedures (single subsampling, CDF pooling, repeated subsampling), author-specific thresholds and the book effect on accuracy (English only). |
| 04 | Downloads the French and German collections and repeats the analyses for all three languages, including texts by authors outside the candidate set and between-novel dispersion of each author. |
| 06 | Robustness checks: feature selection inside each evaluation round, chunk, novel and author weighting, author-level bootstrap, calibration pool sizes, repeated chunk-level splits, five random chunk selections and dispersion at every chunk length. |
| 07 | Main results with the feature list selected inside each evaluation round. |
| 08 | Author-specific (Mondrian) thresholds in all three languages. |
| 09 | Collects the final tables and summary numbers from the previous steps. |
| 10 | Checks whether calibration and test scores are comparable, the effect of training size on accuracy, 100 versus 500 subsamples, and further dispersion checks; records the R session. |
| 05 | Draws the figures. It is placed at the end of the script and runs last. |

Steps 02 and 03 are the first, English-only analyses; the final results come from steps 04 and 06 to 10.

## Data

The novels are openly available in ELTeC (https://github.com/COST-ELTeC). The data are produced by the script itself: step 01 downloads and parses the English collection, and step 04 the French and German collections; both save the parsed texts in the `paper_conformal` folder, so later steps never download them again. Because the ELTeC repositories may change, results obtained from a later download can differ slightly; `novel_list.csv` lists the 300 novels used (collection, ELTeC identifier, author, title, and whether the author is a candidate or an outsider).
