# Comparing model performances for predicting obesity levels

**Authors:** Sebastian Tenorio, Anuoluwapo Akinkunmi, Raghav Haralalka, and Han Bao

A data analysis project for DSCI 522 (Data Science Workflows) in the Master of Data Science program at the University of British Columbia.

## About

We compare a dummy classifier, a decision tree, logistic regression, and a support vector classifier to see how well demographic, family-history, and lifestyle features predict seven weight-status categories. Previous studies have used machine learning for obesity classification (Kaur et al. 2022 and Solomon et al. 2023). We exclude height and weight because the dataset authors used those measurements to calculate the body mass index (BMI) that defines the target labels (Mendoza Palechor and de la Hoz Manotas 2019).

<!-- add the selected model, the metric and held-out test score, how the model compares with the dummy baseline, and what the result means. -->

We use the [UCI Obesity Levels dataset](https://doi.org/10.24432/C5H31Z), which contains 2,111 records based on survey data from Mexico, Peru, and Colombia. Each row represents an individual-level record collected through the survey or generated synthetically. About 77% of the published records are synthetic, which limits what performance on this dataset can tell us about performance on independently collected survey data.

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
uv run quarto render
```

Rendering runs the whole analysis from scratch:
The analysis uses the CSV in `data/raw/`. If the file is missing, the report downloads it from the UCI Machine Learning Repository, which requires an internet connection. 
Rendering regenerates the training and test CSV files in `data/processed/` and writes the HTML report to `reports/obesity-prediction.html`.

## Dependencies

- [uv](https://docs.astral.sh/uv/) (version 0.12 or higher)
- [Quarto CLI](https://quarto.org/) (version 1.10 or higher)
- Python and packages listed in [`pyproject.toml`](pyproject.toml), and their resolved versions are recorded in [`uv.lock`](uv.lock).

## AI use statement

We used **ChatGPT** to double-check our project files against the Milestone 1 requirements and troubleshoot issues with our code and workflow. When we got stuck, we asked for a hint or a concrete next step. We asked AI to act as a tutor by guiding us step by step, explaining the reasoning behind its suggestions, and giving candid feedback on our work.

The authors reviewed, tested, and edited all AI-generated changes and take full responsibility for the contents of this repository.

<!-- add other AI tools and how they were used once confirmed. -->

**Example prompts**

- "Are there any remaining issues with the YAML header, Python setup chunk, or citations?"
- "What does `git pull --ff-only` do, and when should I use it?"

## License

The project code is licensed under the MIT License. The analysis report is licensed under Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0). See [`LICENSE.md`](LICENSE.md).

The [UCI dataset](https://doi.org/10.24432/C5H31Z) is available under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## References

- [Estimation of Obesity Levels Based on Eating Habits and Physical Condition](https://doi.org/10.24432/C5H31Z). (2019). UCI Machine Learning Repository.
- Mendoza Palechor, F., & de la Hoz Manotas, A. (2019). [Dataset for estimation of obesity levels based on eating habits and physical condition in individuals from Colombia, Peru and Mexico](https://doi.org/10.1016/j.dib.2019.104344). *Data in Brief, 25*, 104344.
- Kaur, R., Kumar, R., & Gupta, M. (2022). [Predicting risk of obesity and meal planning to reduce the obese in adulthood using artificial intelligence](https://doi.org/10.1007/s12020-022-03215-4). *Endocrine, 78*(3), 458–469.
- Solomon, D. D., Khan, S., Garg, S., Gupta, G., Almjally, A., Alabduallah, B. I., Alsagri, H. S., Ibrahim, M. M., & Abdallah, A. M. A. (2023). [Hybrid majority voting: Prediction and classification model for obesity](https://doi.org/10.3390/diagnostics13152610). *Diagnostics, 13*(15), 2610.