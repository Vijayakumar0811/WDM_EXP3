### EX3 Implementation of GSP Algorithm In Python
## NAME: VIJAYAKUMAR S
## REG NO: 212224040359
### DATE: 06-02-2026
### AIM: To implement GSP Algorithm In Python.
### Description:
The Generalized Sequential Pattern (GSP) algorithm is a data mining technique used for discovering frequent patterns within a sequence database. It operates by identifying sequences that frequently occur together. GSP works by employing a depth-first search strategy to explore and extract frequent patterns efficiently.
### Steps:
1. <strong>Database Scanning:</strong> GSP scans the sequence database to determine the support of each item in the dataset.
2. <strong>Candidate Generation:</strong> It generates a set of candidate sequences using frequent items found in the previous step.
3. <strong>Pattern Growth:</strong> It extends the candidate sequences by merging them to form longer patterns, checking their support against a user-defined minimum support threshold.
4. <strong>Repeat:</strong> The process continues until no new sequences meet the minimum support threshold.
<p align="justify">
GSP finds application in various domains such as market basket analysis, web usage mining, bioinformatics, and more. For instance, in retail, GSP can identify common purchasing patterns, helping businesses understand customer behavior for targeted marketing or inventory management.
</p>

### Procedure:
<p align="justify">
1. From collections import defaultdict, from itertools import combinations: Imports necessary libraries/modules. defaultdict is
used to create a dictionary with default values and combinations generates all possible combinations of a sequence.</p>
<p align="justify">
2. generate_candidates(dataset, k): Function to generate candidate k-item sequences from a dataset. It loops through each sequence in the
dataset and finds combinations of length k for each sequence, updating their counts in a dictionary.</p>
<p align="justify">
3. gsp(dataset, min_support): Function that implements the Generalized Sequential Pattern (GSP) algorithm. It iterates through increasing
sequence lengths (k) until no new frequent patterns are found. It calls generate_candidates() to find patterns of varying lengths.</p>
<p align="justify">
4. Example dataset for each category: Defines example sequences for top wear, bottom wear, and party wear categories.</p>
<p align="justify">
5. Minimum support threshold: Sets the minimum support count required for a pattern to be considered frequent.</p>
<p align="justify">
6. Perform GSP algorithm for each category: Applies the GSP algorithm for each category using the defined example datasets and the
minimum support threshold.</p>
<p align="justify">
7. Output the frequent sequential patterns for each category: Prints the frequent sequential patterns 
    along with their support counts
for each wear category.</p>
<p align="justify">
8. Visulaize the sequence patterns using matplotlib.
</p>
### Program:

```python

from collections import defaultdict
from itertools import combinations
# Function to generate candidate k-item sequences
def generate_candidates(dataset, k):
    candidates = defaultdict(int)
    for seq in dataset:
        for comb in combinations(seq,k):
            candidates[comb] += 1
    return {item: support for item, support in candidates.items() if support >= min_support}
                
        

    #WRITE YOUR CODE HERE


#Function to perform GSP algorithm
def gsp(dataset, min_support):
    
    fp = defaultdict(int)
    k = 1
    sequences = dataset
    while True:
        candidates = generate_candidates(sequences,k)
        if not candidates:
            break
        fp.update(candidates)
        k += 1
    return fp
  #/WRITE YOUR CODE HERE/


#Example dataset for each category
dataset = [
 ["a","b","c","b","e","c","f","g","a","b","c"],
 ["a","d","b","c","c","f","g","c","h"],
 ["b","c","a","d","e","b","f","c","d","f","g","h"],
 ["c","e","c","e","h"]
 #Add more sequences for top wear
]

#Minimum support threshold
min_support = 5
#Perform GSP algorithm for each category
result = gsp(dataset, min_support)

#Output the frequent sequential patterns for each category
print("Frequent Sequential Patterns - Data Set")
grouped = defaultdict(list)

for pattern, support in result.items():
    grouped[len(pattern)].append((pattern, support))

for k in sorted(grouped.keys()):
    print("\n" + "=" * 45)
    print(f"{k}-Length Frequent Sequences")
    print("=" * 45)
    print(f"| {'Pattern':30} | Support |")
    print("-" * 45)

    for pattern, support in grouped[k]:
        print(f"| {str(pattern):30} | {support:^7} |")

    print("-" * 45)

```
### Output:
<img width="1870" height="910" alt="image" src="https://github.com/user-attachments/assets/09919f4b-dc10-4888-b911-e4c29771678d" />

### Visualization:
```python

import matplotlib.pyplot as plt

# Function to visualize frequent sequential patterns with a line plot
def visualize_patterns_line(result, category):
    if result:
        patterns = list(result.keys())
        support = list(result.values())

        plt.figure(figsize=(10, 6))
        plt.plot([str(pattern) for pattern in patterns], support, marker='o', linestyle='-', color='blue')
        plt.xlabel('Patterns')
        plt.ylabel('Support Count')
        plt.title(f'Frequent Sequential Patterns - {category}')
        plt.xticks(rotation=90)
        plt.tight_layout()
        plt.show()
    else:
        print(f"No frequent sequential patterns found in {category}.")

# Visualize frequent sequential patterns for each category using a line plot
visualize_patterns_line(result, 'Dataset')

```
### Output:

<img width="1794" height="839" alt="image" src="https://github.com/user-attachments/assets/0f9c5649-795d-448e-ad40-bc36229fc96e" />

### Result:
Thus, the GSP algorithm successfully identified frequent sequential patterns of lengths 1 to 4 from the given dataset based on the specified minimum support threshold.
