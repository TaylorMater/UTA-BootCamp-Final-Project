# Predicting Tennis Match Winners 2009-2023 
## Description

## Data Sources
- [tennis_atp by JeffSackman on GitHub](https://github.com/JeffSackmann/tennis_atp)
- [Huge Tennis Database by guillemservera on Kaggle](https://www.kaggle.com/datasets/guillemservera/tennis/data)
## Requirements

- Libraries:
    - pandas
    - scikit-learn
    - tensorflow
    - sqlite3
## Repo Overview
- /resources - contains sqlite database and tables of model performance over different versions
- /keegan-scripts - contains data cleaning notebook and notebooks for random forest classification models
## Installation
Clone the repository: git@github.com:TaylorMater/UTA-BootCamp-Final-Project.git
## Usage

## Data Cleaning
- Filtered out lower level tournaments (Challengers, Satellites/ITFs, and Davis Cup), qualifying rounds, and matches before the 2009 season because that is when the ranking system changed.
- All set scores were in one column, so the scores for each set and each player were separated into their respective columns.
- The match winner and loser stats were located in the same column, so they needed to be split into two separate rows. 
- A column was created to indicate if the player won or lost the match.
## Model Analysis
### Random Forest Classification Model
- A random forest classification model was used to try and predict the outcomes of tennis matches from 2009-2023. The data contains both categorical and numerical features, so this model was chosen because it is able to handle both types of features. The scores for this model were: \
![model scores](/Resources/random_forest_scores.png)
- Before training the model, the numerical features were standardized, missing numerical data points were imputed using the mean, and missing categorical features were imputed using the most frequent value.
- Version 1 of the model was a basic random forest using player name, country code, rank, rank points, age, height, ID, hand, and match stats. 
- Version 2 was a random forest with grid search cv to find the best hyperparameters.
- Version 3 was a random forest with stratified k-fold cross-validation added to the grid search cv to prevent overfitting. The player ID, name, and rank points columns were dropped.
- Version 4 used the same hyperparameter tuning from version 3 and dropped the player rank and country code columns.
- Version 5 used the same hyperparameter tuning from version 3 and dropped the player height, age, and hand columns. The 'F' (Tour Finals) level tournaments were also dropped from the data because set scores only go to 4.
- This model performed well enough that it could be confidently used to predict the outcome of matches using only match stats or match and player stats. The accuracy, precision, recall, F1-score, and ROC AUC are above .8, which is a sign of good predictive power. I would recommend this model to be used in predicting match outcomes using only match stats (version 5) and using match stats and player stats (version 1).
- A future optimization would be to train the model without using the set score to see if the model can still make an accurate prediction. The set score could have caused overfitting, but if the current model is given all the match stats, it still has good predictive power.
## Limitations

## Contributors
- [Riley Taylor](https://github.com/TaylorMater)
- [Michael Spence](https://github.com/michael8607)
- [Rafael Realyvazquez](https://github.com/realyvazquez7)
- [Keegan Davis](https://github.com/KeeganDavis)
## Code Sources
- https://stackoverflow.com/questions/45565311/pandas-interleave-zip-two-dataframes-by-row \
- https://scikit-learn.org/stable/auto_examples/compose/plot_column_transformer_mixed_types.html \
- https://hyperskill.org/learn/step/15401