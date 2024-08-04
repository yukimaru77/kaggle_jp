# Easily Visualize and Compare Prompt, Response and Winner

**Nazim Cherpanov** *Mon May 27 2024 18:42:02 GMT+0900 (日本標準時)* (2 votes)

## Introduction:

When dealing with conversational AI datasets, it's crucial to grasp the quality of the responses produced by various models. In this conversation, I will introduce a useful function that enables you to easily visualize and compare the responses for a specific prompt, as well as the top-performing model.

## Function Overview:

The function get_info_by_id(index) takes an index as input and retrieves the corresponding prompt, responses from two models (Model A and Model B), and the winner from the Kaggle dataset. It then displays the information in an easy-to-read format.

## Code Snippet:

```
train_path = '/kaggle/input/lmsys-chatbot-arena/train.csv'
train = pd.read_csv(train_path, index_col='id').reset_index(drop=True)

ef get_info_by_id(index):
     if index not in list(train.index):
         display("index not in train")
     else:
        print(f"\n{'*'*10} Prompt {'*'*10}\n")
        display(train.iloc[index]['prompt'])

        print(f"\n\n{'*'*10} response A {'*'*10}\n")
        display(train.iloc[index]['response_a'])

        print(f"\n\n{'*'*10} response B {'*'*10}\n")
        display(train.iloc[index]['response_b'])

        print(f"\n\n{'*'*10} Winner {'*'*10}\n")
        if train.iloc[index]['winner_model_a'] == 1:
            display('Model A')
        elif train.iloc[index]['winner_model_b'] == 1:
            display('Model B')
        else:
            display('Tie')`

get_info_by_id(3)

```

## Usage:

To use the function, simply call get_info_by_id() with the desired index from the train dataset. For example, get_info_by_id(3) will display the prompt, responses, and the winner for the row with index 3.

## Happy Kaggling!



