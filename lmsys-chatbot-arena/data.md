# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Dataset Description

The competition dataset consists of user interactions from the [ChatBot Arena](https://chat.lmsys.org/). In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response. The goal of the competition is to predict the preferences of the judges and determine the likelihood that a given prompt/response pair is selected as the winner.

Please note that this is a [Code Competition](https://www.kaggle.com/competitions/lmsys-chatbot-arena/overview/code-requirements). When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

## Files

train.csv 

- id - A unique identifier for the row.

- model_[a/b] - The identity of model_[a/b]. Included in train.csv but not test.csv.

- prompt - The prompt that was given as an input (to both models).

- response_[a/b] - The response from model_[a/b] to the given prompt.

- winner_model_[a/b/tie] - Binary columns marking the judge's selection. The ground truth target column.

test.csv 

- id

- prompt

- response_[a/b]

sample_submission.csv A submission file in the correct format.

- id

- winner_model_[a/b/tie] - This is what is predicted from the test set.

Note: the dataset for this competition contains text that may be considered profane, vulgar, or offensive.

## Files

3 files

## Size

184.19 MB

## Type

csv

## License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

### sample_submission.csv(237 B)

get_appfullscreenchevron_rightNew entrants are currently not allowed. You will be able to accept the rules and view the data after the competition completes.

## Data Explorer

184.19 MB

- calendar_view_weeksample_submission.csv

- calendar_view_weektest.csv

- calendar_view_weektrain.csv

## Summary

arrow_rightfolder3 files

arrow_rightcalendar_view_week17 columns

get_appDownload Allnavigate_nextminimizekaggle competitions download -c lmsys-chatbot-arenacontent_copyhelpDownload datatext_snippet## Metadata

### License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Dataset Description

The competition dataset consists of user interactions from the [ChatBot Arena](https://chat.lmsys.org/). In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response. The goal of the competition is to predict the preferences of the judges and determine the likelihood that a given prompt/response pair is selected as the winner.

Please note that this is a [Code Competition](https://www.kaggle.com/competitions/lmsys-chatbot-arena/overview/code-requirements). When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

## Files

train.csv 

- id - A unique identifier for the row.

- model_[a/b] - The identity of model_[a/b]. Included in train.csv but not test.csv.

- prompt - The prompt that was given as an input (to both models).

- response_[a/b] - The response from model_[a/b] to the given prompt.

- winner_model_[a/b/tie] - Binary columns marking the judge's selection. The ground truth target column.

test.csv 

- id

- prompt

- response_[a/b]

sample_submission.csv A submission file in the correct format.

- id

- winner_model_[a/b/tie] - This is what is predicted from the test set.

Note: the dataset for this competition contains text that may be considered profane, vulgar, or offensive.

## Files

3 files

## Size

184.19 MB

## Type

csv

## License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

### sample_submission.csv(237 B)

get_appfullscreenchevron_rightNew entrants are currently not allowed. You will be able to accept the rules and view the data after the competition completes.

## Data Explorer

184.19 MB

- calendar_view_weeksample_submission.csv

- calendar_view_weektest.csv

- calendar_view_weektrain.csv

## Summary

arrow_rightfolder3 files

arrow_rightcalendar_view_week17 columns

get_appDownload Allnavigate_nextminimizekaggle competitions download -c lmsys-chatbot-arenacontent_copyhelpDownload datatext_snippet## Metadata

### License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

# LMSYS - Chatbot Arena Human Preference Predictions

Predicting Human Preferences in the Wild



[Overview](/competitions/lmsys-chatbot-arena/overview)　[Data](/competitions/lmsys-chatbot-arena/data)　[Code](/competitions/lmsys-chatbot-arena/code)　[Models](/competitions/lmsys-chatbot-arena/models)　[Discussion](/competitions/lmsys-chatbot-arena/discussion)　[Leaderboard](/competitions/lmsys-chatbot-arena/leaderboard)　[Rules](/competitions/lmsys-chatbot-arena/rules)　

## Dataset Description

The competition dataset consists of user interactions from the [ChatBot Arena](https://chat.lmsys.org/). In each user interaction a judge provides one or more prompts to two different large language models, and then indicates which of the models gave the more satisfactory response. The goal of the competition is to predict the preferences of the judges and determine the likelihood that a given prompt/response pair is selected as the winner.

Please note that this is a [Code Competition](https://www.kaggle.com/competitions/lmsys-chatbot-arena/overview/code-requirements). When your submission is scored, this example test data will be replaced with the full test set. There are 55K rows in the training data, and you can expect roughly 25,000 rows in the test set.

## Files

train.csv 

- id - A unique identifier for the row.

- model_[a/b] - The identity of model_[a/b]. Included in train.csv but not test.csv.

- prompt - The prompt that was given as an input (to both models).

- response_[a/b] - The response from model_[a/b] to the given prompt.

- winner_model_[a/b/tie] - Binary columns marking the judge's selection. The ground truth target column.

test.csv 

- id

- prompt

- response_[a/b]

sample_submission.csv A submission file in the correct format.

- id

- winner_model_[a/b/tie] - This is what is predicted from the test set.

Note: the dataset for this competition contains text that may be considered profane, vulgar, or offensive.

## Files

3 files

## Size

184.19 MB

## Type

csv

## License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

### sample_submission.csv(237 B)

get_appfullscreenchevron_rightNew entrants are currently not allowed. You will be able to accept the rules and view the data after the competition completes.

## Data Explorer

184.19 MB

- calendar_view_weeksample_submission.csv

- calendar_view_weektest.csv

- calendar_view_weektrain.csv

## Summary

arrow_rightfolder3 files

arrow_rightcalendar_view_week17 columns

get_appDownload Allnavigate_nextminimizekaggle competitions download -c lmsys-chatbot-arenacontent_copyhelpDownload datatext_snippet## Metadata

### License

[Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)](https://creativecommons.org/licenses/by-nc/4.0/)

