# There is more than 1 prompt in ~10% of the ['prompt'] rows

**Matthew Hendricks** *Fri Jul 12 2024 02:04:16 GMT+0900 (日本標準時)* (1 votes)



```
import matplotlib.pyplot as plt
from datasets import load_dataset
import ast

# Load the dataset
dataset = load_dataset("lmsys/lmsys-arena-human-preference-55k", split='train')

# Function to safely evaluate the string as a list
def safe_eval(s):
    try:
        return ast.literal_eval(s)
    except:
        return []

# Count the number of items in each prompt
item_counts = [len(safe_eval(prompt)) for prompt in dataset['prompt']]

# Count the frequency of each number of items
count_freq = {}
for count in item_counts:
    count_freq[count] = count_freq.get(count, 0) + 1

# Prepare data for plotting
counts = list(count_freq.keys())
frequencies = list(count_freq.values())

# Create the bar plot
plt.figure(figsize=(10, 6))
plt.bar(counts, frequencies)
plt.xlabel('Number of Items in Prompt')
plt.ylabel('Frequency')
plt.title('Distribution of Number of Items in Prompts')
plt.xticks(range(min(counts), max(counts)+1))

# Add value labels on top of each bar
for i, v in enumerate(frequencies):
    plt.text(counts[i], v, str(v), ha='center', va='bottom')

plt.tight_layout()
plt.show()

# Print some statistics
total_prompts = len(item_counts)
avg_items = sum(item_counts) / total_prompts
print(f"Total number of prompts: {total_prompts}")
print(f"Average number of items per prompt: {avg_items:.2f}")
print(f"Most common number of items: {max(count_freq, key=count_freq.get)}")
print(f"Maximum number of items in a prompt: {max(counts)}")

```



