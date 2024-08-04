# Clean Text

**TheStoneMX** *Sun Jul 14 2024 07:21:59 GMT+0900 (日本標準時)* (3 votes)

Hi there all,

I have been trying different text-cleaning techniques, but they do not work… can someone share? or is there no text cleaning on these types of corpus?

Or what other ways to increase the score besides the Ensemble models?

Thanks!

Like:

```
import pandas as pd
import re
from datasets import Dataset

def load_and_clean_data(filepath):
    # Load dataset
    df = pd.read_csv(filepath)

    # Remove duplicates
    df.drop_duplicates(inplace=True)

    # Handle missing values (replace NaN with empty string)
    df.fillna("", inplace=True)

    # Clean text function
    def clean_text(text):
        # Convert to string in case of any non-string values
        text = str(text)

        # Remove unwanted characters
        text = re.sub(r'[\[\]\'"]', '', text)  # Corrected regular expression

        # Remove punctuation and special characters except periods, commas, apostrophes, and double quotes
        text = re.sub(r'[^\w\s\.,\'\"]', '', text)       
        text = text.lower() # Convert to lowercase
        text.strip()  # strip leading/trailing spaces

        # Remove URLs and Email Addresses
        text = re.sub(r'\b(?:https?://|www\.)\S+\b', '', text)
        text = re.sub(r'\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Z|a-z]{2,}\b', '', text)
         # Remove numbers
        text = re.sub(r'\d+', '', text)

        return text

    # Clean text columns
    df['prompt'] = df['prompt'].apply(clean_text)
    df['response_a'] = df['response_a'].apply(clean_text)
    df['response_b'] = df['response_b'].apply(clean_text)

    return df

# Load and clean the data
df_cleaned = load_and_clean_data("../input/lmsys-chatbot-arena/train.csv")

# Convert to Hugging Face Dataset
ds = Dataset.from_pandas(df_cleaned)

# Print the first row 
print(ds[:1])

```



---

 # Comments from other users

> ## Bharat Raghavan
> 
> It seems to me like your code manages to clean up the text properly, unless you want to clean it further; in that case, what text-cleaning techniques are you talking about?
> 
> As for increasing the score, depending on the approach, hyperparameter tuning can be beneficial. However, I would just recommend that you be wary of overfitting when considering your approach to hyperparameter tuning.
> 
> 
> 


---

