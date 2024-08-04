# Llama 3.1 Hack - Confirmed to Work in Kaggle Environment (Notebooks and Competition)

**Matthew S Farmer** *Fri Aug 02 2024 04:34:42 GMT+0900 (日本標準時)* (17 votes)

# Llama 3.1

So, you saw the latest release of Llama 3.1 and thought to yourself "I bet this would be good in the LLM 20 Questions competition". Then you fired up a notebook, imported the model, attempted to load it, then were faced with an error about RoPE scaling… You jump on the discussion board and don't find any help. You look online and all the posts say "update transformers". You do that and the notebook works, but then you get that pesky validation error. What are we to do! As any tinkerers or hackers know, there's always a workaround somewhere…

## We have a workaround!

I have validated that this works in the notebook and game environment without updating transformers. 

```
import json
with open("YOUR_LOCAL_MODEL_PATH/config.json", "r") as file:
    config = json.load(file)
config["rope_scaling"] = {"factor":8.0,"type":"dynamic"}
with open("YOUR_LOCAL_MODEL_PATH/config.json", "w") as file:
    json.dump(config, file)

```

## Implementation

Remove any updates to transformers that you were trying.
Import your desired llama 3.1 model to your working folder
Validate the path to config.json in that folder and replace the all caps path in the code above.
Add the code in a code block that precedes your submission .py script and tarball submission. 
Load the model and script as you normally would. 
Validate text generation in the notebook if desired.
Prepare your script for submission, ensuring that the updated config file is zipped with the model. 
Enjoy the green checkmark after validation. 

I hope this raises the bar for everyone in this competition as we approach the final evaluation. May the best agents win!

## TL;DR

Modify config.json to a dictionary that the current version of Transformers expects (2 fields). 

Cheers! Happy Kaggling 

If you have questions about RoPE scaling, check out [the docs! ](https://huggingface.co/docs/text-generation-inference/en/basic_tutorials/preparing_model)



---

 # Comments from other users

> ## VolodymyrBilyachat
> 
> Legend! thank you for this simple hack :)
> 
> 
> 


---

