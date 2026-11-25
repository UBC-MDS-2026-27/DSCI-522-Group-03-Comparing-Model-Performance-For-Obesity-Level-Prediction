# Comparing model performances for predicting obesity levels

**Authors:** Sebastian Tenorio, Anuoluwapo Akinkunmi, Raghav Haralalka, and Han Bao

A data analysis project for DSCI 522 (Data Science Workflows) in the Master of Data Science program at the University of British Columbia.

## About

We compared a dummy classifier, logistic regression, and a support vector classifier with a radial basis function kernel (RBF SVC) to predict seven weight-status categories from demographic, family history, and lifestyle features. We excluded height and weight because the dataset authors used those measurements to calculate the body mass index (BMI) that defined the target labels (Mendoza Palechor and de la Hoz Manotas 2019). The RBF SVC performed best in five-fold cross-validation. On the held-out test set, it achieved a macro F1 score of 0.787, compared with 0.041 for the dummy classifier, and correctly classified 498 of 634 records (78.5%). The model tended to overpredict normal weight. Of the 139 records it assigned to that category, 67 were actually labelled normal weight. Because about 77% of the dataset is synthetic, performance on independently collected survey data remains uncertain.

We use the [UCI Obesity Levels dataset](https://doi.org/10.24432/C5H31Z), which contains 2,111 records based on survey data from Mexico, Peru, and Colombia. Each row represents an individual-level record collected through the survey or generated synthetically. The variables include age, gender, family history of overweight, eating habits, and physical activity. The response is the recorded weight-status category, ranging from insufficient weight to obesity type III.

## Report

The final report can be found [here](https://ubc-mds-2026-27.github.io/DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction/) (HTML), or as a [PDF](reports/obesity-prediction.pdf)

## Usage

The analysis runs in a Docker container so everyone uses the same software and package versions. The image is available on [Docker Hub](https://hub.docker.com/r/humphreybao/dsci-522-group-03-comparing-model-performance-for-obesity-level-prediction).


### Setup

First time running the project, install and launch [Docker](https://www.docker.com/get-started/). Then use Git to clone the repository and enter its root directory.

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction.git
cd DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction
```

Run all the commands below from the root of this repository.

### 1. Make an SSH key

If you don't have an ssh key yet, make one and press Enter at each question:

```bash
ssh-keygen -t ed25519
```

The container lets you log in with this key. If you skip this step, Docker makes a folder named ~/.ssh/id_ed25519.pub instead, and connecting to the container over ssh fails until you delete that folder and make the key.

### 2. Download the image

```bash
docker compose pull
```

### 3. Run the analysis and render the report

```bash
docker compose run --rm analysis-env uv run quarto render
```

The analysis uses the CSV in `data/raw/` and downloads it from the UCI Machine Learning Repository if it is missing. The run regenerates the training, test, and preprocessed CSVs in `data/processed/`, then replaces `reports/obesity-prediction.html` and `reports/obesity-prediction.pdf` with the rendered reports. The `--rm` flag automatically removes the temporary container when the command finishes.

## Contributing

To develop inside the container, add a package, or update the published report, see [`CONTRIBUTING.md`](CONTRIBUTING.md).

## Dependencies

- [Docker](https://www.docker.com/)
- The image is built from the [`Dockerfile`](Dockerfile) in this repository.
  It installs Quarto, uv,
  and Python with the packages listed in [`pyproject.toml`](pyproject.toml)
  (exact versions are locked in [`uv.lock`](uv.lock)).

## AI use statement

We used **ChatGPT** and **Claude (Anthropic)** to double-check our project files against the Milestone 1 requirements, debug code and workflow issues, and get hints when we got stuck. We asked AI to act as a tutor by guiding us step by step, explaining the reasoning behind its suggestions, and giving candid feedback on our work.

The authors reviewed, tested, and edited all AI-generated changes and take full responsibility for the contents of this repository.

**Example prompts**

- "Are there any remaining issues with the YAML header, Python setup chunk, or citations?"
- "What does `git pull --ff-only` do, and when should I use it?"
- "I have started my work, I already created a branch locally and i have editted the code of conduct .md file. However, i did a merging on the comment regarding the report. Do i need to pull again since there might be changes when i want to push, What do you advice just to avoid merge conflicts."
- "Instead of me saying almost always 3, can i use proportion, then the 2 charts in the middle of my plot is shifted, anything wrong with my code?"

## License

The project code is licensed under the MIT License. The analysis report is licensed under Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0). See [`LICENSE.md`](LICENSE.md).

The [UCI dataset](https://doi.org/10.24432/C5H31Z) is available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## References

- [Estimation of Obesity Levels Based on Eating Habits and Physical Condition](https://doi.org/10.24432/C5H31Z). (2019). UCI Machine Learning Repository.
- Kaur, R., Kumar, R., & Gupta, M. (2022). [Predicting risk of obesity and meal planning to reduce the obese in adulthood using artificial intelligence](https://doi.org/10.1007/s12020-022-03215-4). *Endocrine, 78*(3), 458–469.
- Mendoza Palechor, F., & de la Hoz Manotas, A. (2019). [Dataset for estimation of obesity levels based on eating habits and physical condition in individuals from Colombia, Peru and Mexico](https://doi.org/10.1016/j.dib.2019.104344). *Data in Brief, 25*, 104344.
- Solomon, D. D., Khan, S., Garg, S., Gupta, G., Almjally, A., Alabduallah, B. I., Alsagri, H. S., Ibrahim, M. M., & Abdallah, A. M. A. (2023). [Hybrid majority voting: Prediction and classification model for obesity](https://doi.org/10.3390/diagnostics13152610). *Diagnostics, 13*(15), 2610.
- Zhang, J. (2025). [Machine learning analysis of obesity levels based on lifestyle and physical features](https://doi.org/10.54254/2753-8818/2025.AU27039). *Theoretical and Natural Science, 135*, 90–98.
- Harris, C. R., Millman, K. J., van der Walt, S. J., et al. (2020). [Array programming with NumPy](https://doi.org/10.1038/s41586-020-2649-2). *Nature, 585*, 357–362.
- McKinney, W. (2010). [Data structures for statistical computing in Python](https://doi.org/10.25080/Majora-92bf1922-00a). In *Proceedings of the 9th Python in Science Conference* (pp. 56–61).
- Pedregosa, F., Varoquaux, G., Gramfort, A., et al. (2011). Scikit-learn: Machine learning in Python. *Journal of Machine Learning Research, 12*, 2825–2830.
- Reitz, K. (2011). [Requests: HTTP for humans](https://requests.readthedocs.io/). https://requests.readthedocs.io/
- Van Rossum, G., & Drake, F. L. (2009). *Python 3 reference manual*. Scotts Valley, CA: CreateSpace.
- VanderPlas, J., Granger, B. E., Heer, J., et al. (2018). [Altair: Interactive statistical visualizations for Python](https://doi.org/10.21105/joss.01057). *Journal of Open Source Software, 3*(32), 1057.
