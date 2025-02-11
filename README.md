# Note
This model was built using `mlr3verse` version `0.2.8` and `paradox` version `0.11.1`. Please ensure that the correct versions of these R packages are installed before using the model, as mismatched versions may lead to unforeseen errors.
# ColonTrack
A machine learning model for `CRC` diagnosis
The model has been trained on extensive clinical ELISA data to achieve high-performance discrimination of colorectal cancer. It shows great potential for early colorectal cancer diagnosis.
In brief, to diagnose new samples, the concentrations of `CTTN`, `HNRNPK`, and `PSMC6` in plasma EVs must first be measured using the ELISA. The concentration values are reported in `ng/mL`. These three protein concentrations are then input into the ColonTrack model, which calculates a score based on these values. If the score is greater than or equal to 0.5, the sample is classified as `CRC`; otherwise, it is classified as `non-CRC`.


The `ColonTrack.rds` file is a machine learning model file built using the R `mlr3` package. The `trails_data.csv` file contains the data used for model training.
```r
# R code example
ColonTrack <- readRDS("path/to/ColonTrack.rds")
trails_data <- read.csv("path/to/trails_data.csv")


predict = ColonTrack$predict_newdata(newdata = trais_data)
trais_data |> 
  dplyr::mutate(ColonTrack = predict$prob[, 1])
```
```
> trais_data |> 
+     dplyr::mutate(ColonTrack = predict$prob[, 1])
       Sample   CTTN HNRNPK PSMC6   ColonTrack
1     Sample1   0.11   0.00  0.72 0.0093333333
2     Sample2   0.13   0.60  0.94 0.0042666667
3     Sample3   0.11   1.14  0.56 0.0020000000
4     Sample4   0.15   1.65  0.44 0.0056333333
5     Sample5   0.26   0.10  0.60 0.0004000000
6     Sample6   0.12   0.00  1.23 0.0508333333
7     Sample7   2.77   1.86  0.56 0.4271333333
8     Sample8   0.13   0.51  0.54 0.0059333333
9     Sample9   0.14   0.00  0.92 0.0162095238
10   Sample10   0.11   0.62  0.84 0.0000000000
```

The original ColonTrack model was trained using a dataset from a single center, consisting of 123 `CRC` patients and 118 `non-CRC` controls. Despite the model showing an accuracy greater than 90% in over 800 samples, the limited sample size and single-center origin of the dataset may introduce some bias, and the model may not fully represent the broader characteristics of CRC. Therefore, its generalizability and robustness require further investigation.
To improve upon this limitation, we trained a new model, ColonTrack-Pro, using ELISA data from four centers, with 557 CRC and 545 non-CRC samples. ColonTrack-Pro is also available for open-source use on GitHub. While this model has not yet been validated with external cohorts, it holds promise for broader diagnostic applications and serves as a valuable reference for future validation efforts.

# MIT License with Non-Commercial Clause

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, subject to the following conditions:

This Model is for educational and research purposes only. Commercial use is prohibited without explicit written permission from the author.

(MIT License content follows)
