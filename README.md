# Building Spam Filter using Naive Bayes Algorithm
## About the dataset
The dataset of 5,572 SMS messages that are already classified by humans was put together by Tiago A. Almeida and José María Gómez Hidalgo, and it can be downloaded from the [The UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/sms+spam+collection).

## Steps taken
1)	Randomise data before splitting data into 80% training set and 20% test set
2)	Check that the percentage of spam/ham in each training and test set is similar to the original 100% data.
3)	Data clean SMS messages by removing punctuations, lowercase, and splitting
4)	**Create a vocabulary list of unique words** for each split SMS messages, with the goal of creating a dataframe of word counts for each sms
5)	Create **‘unique word : word count in each sms’  key-pair dictionary**, using vocabulary list to count how many times the unique word appear in each sms
6)	**Final training set**: transform **word counts per sms dictionary** into dataframe and concat with to original training set
7)	**Split spam and ham data** from final training set into separate dataframes
8)	Inspect Naïve Bayes Algorithm to see what are **the constants and parameters to be calculated**. 
      -	Naïve Bayes algorithm will require **probability of Spam/Ham messages(constant)**, and **conditional probability of each word** in the test message which we will call it **parameters**
      -	Parameters will require a set of **constants (probability of Spam/Ham messages, Number of words in all spam/ham messages, Number of vocabulary)**
9)	Calculate constants using len() and sum() to spam/ham dataframes 
10)	For parameters (conditional probability of word given spam/ham message), **the goal is to save the probability to each unique word in a key-value pair dictionary to retrieve it using the unique word key later**.
11)	Initiate a **‘unique word: parameter’  key-value pair dictionary**. 
12)	Loop through vocabulary and for each unique word, 
    -	sum word count found in ALL spam/ham dataframe, 
    -	apply word count to conditional probability formula using constants calculated earlier, 
    -	then assign conditional probability result to the spam/ham parameter dictionary
13)	**Write a function to automate the algorithm steps above**:
    -	Takes a string input as new message and perform data cleaning
    -	Calculate probability of spam/ham given the message using naïve bayes algorithm and by looping through each word in the message, if word in parameter dictionary key created earlier, multiply the paired probability value to probability of spam/ham messages
    
    **Eg**. p_spam_given_message = p_spam(constant calculated earlier) * word_1 probability in spam parameter dictionary *word_2 probability in spam parameter dictionary

    **Eg**. P_ham_given_message = p_ham(constant calculated earlier)  * word_1 probability in ham parameter dictionary *word_2 probability in ham parameter dictionary

    -	Compare probability of spam to probability of ham to classify whether it is a ham/spam/require human help
    -	Return label ‘spam’ or ‘ham’ or ‘needs human classification’

14)	Using on test set, we will create a new ‘predicted’ column to store these classification labels when we apply the function to the test dataframe.
15)	**Calculate accuracy**, we will use number of correctly classified messages divide by total number of classified message. 
16)	To count number of correctly classified messages, we can loop through test dataframe and compare ‘label’ column with ‘predicted’ column, for each row that is equivalent, then increment correct count by 1

## Checking outliers and limiations of algorithm
There are 14 messages that were not classified correctly, detailed analysis and visualisation were done for 3 messages to understand the cause of misclassification.

