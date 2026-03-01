# Assessing Working Memory Capacity of Large Language Models (LLMs) Using N-back Tasks

![image](https://github.com/user-attachments/assets/f968575a-00be-4453-bc62-5d9237fa26fe)

This repository contains the code and data for reproducing the experiments on ChatGPT's working memory capacity using verbal N-back tasks. This work is based on the paper "Working Memory Capacity of ChatGPT: An Empirical Study" (AAAI 2024).
<img width="777" height="359.8" alt="image" src="https://github.com/user-attachments/assets/e9bc8458-6501-43d0-bf21-bfa8a46feedf" />
<img width="777" height="222.8" alt="image" src="https://github.com/user-attachments/assets/232b2ecf-880f-4967-a5f8-8bc5b04d6dba" />


🔧 Installation  
Prerequisites  
Python 3.9+  
Anaconda (recommended) or pip  
OpenAI API key  

Setup Environment
```
# Clone the repository
git clone https://github.com/xuruoxuan086-dotcom/FTEC5660.git
cd FTEC5660/homeworks/Individual\ Project

# Create conda environment (recommended)
conda create -n wm python=3.9
conda activate wm

# Install dependencies
pip install openai numpy pandas scipy matplotlib seaborn jupyter
```
📊 Dataset
We created a dataset to test the working memory capacity of language models using the N-back task, which is widely used in cognitive science as a measure of working memory capacity.

Dataset Structure  
For each N-back level ($N = {1, 2, 3}$), we generated 50 blocks of trials (modified from the original paper's 30 blocks). Each block contains 24 trials, including 8 match trials and 16 nonmatch trials.  
The dataset for each block is stored in a text file with the following format:  
Line 1: The letter sequence presented on each trial  
Line 2: The condition for each letter ('m' for match trial, '-' for nonmatch trial)  


For the base version of verbal N-back tasks, we use the following prompt format for $N = {1, 2, 3}$:  

**Prompt Example.** Here we only focus on the base version of verbal N-back tasks. We use the following format of prompts for $N = \{1, 2, 3\}$:  
1-back Task:
```
User:
Instruction: as a language model, you are asked to perform a 1-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the previous letter, and '-' whenever the letter presented is different from the previous letter. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

2-back Task:
```
User:
Instruction: as a language model, you are asked to perform a 2-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter two trials ago, and '-' whenever the letter presented is different from the letter two trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

3-back Task:
```
User:
Instruction: as a language model, you are asked to perform a 3-back task. A letter will be presented on every trial. Your task is to respond with 'm' whenever the letter presented is the same as the letter three trials ago, and '-' whenever the letter presented is different from the letter three trials ago. A strict rule is that you must not output anything other than 'm' or '-'. Now begins the task.

User:
{letter}
Model:
{-}(because this is the first letter)

User:
{letter}
Model:
{m/-}

...
```

Open and run the following notebooks in order:  

verbal.ipynb - Baseline N-back tasks (n=1,2,3) at temperature=1.0  
verbal - low-temperature.ipynb - Experiments at temperature=0.2  
verbal - high-temperature.ipynb - Experiments at temperature=1.5  

📊 Metrics Calculation  
The following metrics are calculated for each experiment:  
Metric	Definition  
Hit Rate：Proportion of match trials correctly responded with "m"  
False Alarm Rate：Proportion of nonmatch trials incorrectly responded with "m"  
Accuracy：Overall proportion of correct responses  
d' (Detection Sensitivity)：z(Hit Rate) - z(False Alarm Rate)  
