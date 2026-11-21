# Comparing model performances for predicting obesity levels

**Authors:** Sebastian Tenorio, Anuoluwapo Akinkunmi, Raghav Haralalka, and Han Bao

A data analysis project for DSCI 522 (Data Science Workflows) in the Master of Data Science program at the University of British Columbia.

## About

We compared a dummy classifier, logistic regression, and a support vector classifier with a radial basis function kernel (RBF SVC) to predict seven weight-status categories from demographic, family history, and lifestyle features. We excluded height and weight because the dataset authors used those measurements to calculate the body mass index (BMI) that defined the target labels (Mendoza Palechor and de la Hoz Manotas 2019). The RBF SVC performed best in five-fold cross-validation. On the held-out test set, it achieved a macro F1 score of 0.787, compared with 0.041 for the dummy classifier, and correctly classified 498 of 634 records (78.5%). The model tended to overpredict normal weight. Of the 139 records it assigned to that category, 67 were actually labelled normal weight. Because about 77% of the dataset is synthetic, performance on independently collected survey data remains uncertain.

We use the [UCI Obesity Levels dataset](https://doi.org/10.24432/C5H31Z), which contains 2,111 records based on survey data from Mexico, Peru, and Colombia. Each row represents an individual-level record collected through the survey or generated synthetically. The variables include age, gender, family history of overweight, eating habits, and physical activity. The response is the recorded weight-status category, ranging from insufficient weight to obesity type III.

## Report

The final report can be found here 
[HTML](https://github.com/UBC-MDS-2026-27/DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction/blob/main/reports/obesity-prediction.html)
<!-- check url after the final report-->

## Usage

Install [uv](https://docs.astral.sh/uv/getting-started/installation/) and [Quarto](https://quarto.org/docs/get-started/). Then clone the repository and open its root directory in your terminal.

```bash
git clone https://github.com/UBC-MDS-2026-27/DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction.git
cd DSCI-522-Group-03-Comparing-Model-Performance-For-Obesity-Level-Prediction
```
Then run the following from the root of this repository to create the virtual environment:

``` bash
uv sync
```

To run the analysis and render the report, run the following from the root of this repository:

``` bash
uv run quarto render reports/obesity-prediction.qmd
```

Rendering runs the whole analysis from scratch:
The analysis uses the CSV in `data/raw/`. If the file is missing, the report downloads it from the UCI Machine Learning Repository, which requires an internet connection. 
Rendering regenerates the training and test CSV files in `data/processed/` and writes the HTML report to `reports/obesity-prediction.html`.

## Dependencies

- [uv](https://docs.astral.sh/uv/) (version 0.12 or higher)
- [Quarto CLI](https://quarto.org/) (version 1.10 or higher)
- Python and packages listed in [`pyproject.toml`](pyproject.toml), and their resolved versions are recorded in [`uv.lock`](uv.lock).

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
- Mendoza Palechor, F., & de la Hoz Manotas, A. (2019). [Dataset for estimation of obesity levels based on eating habits and physical condition in individuals from Colombia, Peru and Mexico](https://doi.org/10.1016/j.dib.2019.104344). *Data in Brief, 25*, 104344.
- Kaur, R., Kumar, R., & Gupta, M. (2022). [Predicting risk of obesity and meal planning to reduce the obese in adulthood using artificial intelligence](https://doi.org/10.1007/s12020-022-03215-4). *Endocrine, 78*(3), 458–469.
- Solomon, D. D., Khan, S., Garg, S., Gupta, G., Almjally, A., Alabduallah, B. I., Alsagri, H. S., Ibrahim, M. M., & Abdallah, A. M. A. (2023). [Hybrid majority voting: Prediction and classification model for obesity](https://doi.org/10.3390/diagnostics13152610). *Diagnostics, 13*(15), 2610.
- Zhang, J. (2025). [Machine learning analysis of obesity levels based on lifestyle and physical features](https://doi.org/10.54254/2753-8818/2025.AU27039). *Theoretical and Natural Science, 135*, 90–98.