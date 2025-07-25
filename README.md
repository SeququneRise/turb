# Fake News Detection

Fake News Detection in Python

This project is part of CS410:Text Information System course. In this project, we have used various natural language processing techniques and machine learning algorithms to classifty fake news articles using sci-kit libraries from python. 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them:

1. Python 3.6 

* This setup requires that your machine has python 3.6 installed on it. you can refere to this https://www.python.org/downloads/ to download python. Once you have python installed, you will need to setup PATH variables. To do that check this: https://www.pythoncentral.io/add-python-to-path-python-is-not-recognized-as-an-internal-or-external-command/

* Optionally you can use anaconda in one step and use its anaconda prompt to run the commands. To install anaconda check this:
https://www.anaconda.com/download/


#### Dataset used
The data source used for this project is taken from LIAR dataset which has 3 files with .tsv format for test, train and validation. Below is some description about the data files used for this project.
	
LIAR: A BENCHMARK DATASET FOR FAKE NEWS DETECTION

William Yang Wang, "Liar, Liar Pants on Fire": A New Benchmark Dataset for Fake News Detection, to appear in Proceedings of the 55th Annual Meeting of the Association for Computational Linguistics (ACL 2017), short paper, Vancouver, BC, Canada, July 30-August 4, ACL.

the original dataset contained 13 variables/columns for train, test and validation sets as follows:

* Column 1: the ID of the statement ([ID].json).
* Column 2: the label. (Label class contains: True, Mostly-true, Half-true, Barely-true, FALSE, Pants-fire)
* Column 3: the statement.
* Column 4: the subject(s).
* Column 5: the speaker.
* Column 6: the speaker's job title.
* Column 7: the state info.
* Column 8: the party affiliation.
* Column 9-13: the total credit history count, including the current statement.
* 9: barely true counts.
* 10: false counts.
* 11: half true counts.
* 12: mostly true counts.
* 13: pants on fire counts.
* Column 14: the context (venue / location of the speech or statement).

To make things simple we have chosen only 2 variables from this original dataset for this classification. The other variables can be added later to add some more complexity and enhance the features.

Below are the colomns used to create 3 datasets that have been in used in this project
* Column 1: Statement (News headline or text).
* Column 2: Label (Label class contains: True, False)
 
You will see that newly created dataset has only 2 classes as compared to 6 from original classes. Below is method used for reducing the number of classes.

* Original 	--	New
* True	   	--	True
* Mostly-true	-- 	True
* Half-true	-- 	True
* Barely-true	-- 	False
* False		-- 	False
* Pants-fire	-- 	False

The dataset used for this project were in csv format named train.csv, test.csv and valid.csv and can be found in repo. The original datasets are in "liar" folder in tsv format.

![alt text](https://github.com/nishitpatel01/Fake_News_Detection/blob/master/Project%20-%20cs410.jpg)


### File descriptions

#### DataPrep.py
This file contains all the pre processing functions needed to process all input documents and texts. First we read the train, test and validation data files then performed some pre processing like tokenizing, stemming etc. There are some exploratory data analysis is performed like response variable distribution and data quality checks like null or missing values etc.

#### FeatureSelection.py
In this file we have performed feature extraction and selection methods from sci-kit learn python libraries. For feature selection, we have used methods like simple bag-of-words and n-grams and then term frequency like tf-tdf weighting. we have also used word2vec and POS tagging to extract the feature, though POS tagging and word2vec has not been used at this point due to the siez of pre-trained word2vec vector.

#### classifier.py
Here we have build all the classifiers for predicting the fake news detection. The extracted features are fed into different classfiers. We have used Naive-bayes, Logistic Regression, Linear SVM, Stochastic gradient decent and Random forest classifiers from sklearn. Each of the extracted featues were used in all of the classifiers. Once fitting the model, we compared the f1 score and checked the confusion matrix. After fitting all the classifiers, 2 best peforming models were selected as candidate models for fake news classification. We have performed parameter tuning by implementing GridSearchCV methos on these candidate models and chosen best performing paramters for these classifier. Finally selected model was used for fake news detection with the probability of truth. In Addition to this, We have also extracted the top 50 features from our term-frequency tfidf vectorizer to see what words are most and important in each of the classes. We have also used learning curves to see how training and test set performs when we increase the amount of data in our classifiers.

#### prediction.py
Our finally selected and best performnig classifer was ```Logistic Regression``` which was then saved on disk with name ```final_model.sav```. Once you close this repository, this model will be copied to user's machine and will be used by prediction.py file to classify the fake news. It takes an news article as input from user then model is used for final classification output that is shown to user along with probability of truth.

To looks the overall process flow of how the program and model is implemented, please take look at the Process-flow.jpg file from repo.

### Performances

### Next steps
As we can see that our best performing models had an f1 score in the range of 70's. This is due to less number of data that we have used for training purposes and simplicity of our models. For the future implementations, we could introduce some more feature selection methods such as POS tagging, word2vec and topic modeling. In addition, we could also increase the training data size. We will extend this project to implement these techniques in future to increase the accuracy and performance of our models.


### Installing

A step by step series of examples that tell you have to get a development env running

1. The first step would be to clone this repo to your local machine. To do that you need to run following command in command prompt or in git bash
```
$ git clone https://github.com/nishitpatel01/Fake_News_Detection.git
```

2. This will copy all the data source file, program files and model into your machine.

3. After all the files are saved in a folder in your machine. open the anaconda prompt or command line (to setup command line please refer above section "Prerequisites") and type below command and press enter.
```
python prediction.py
```

4. After hitting the enter, program will ask for an input which will be a piece of information or a news headline that you want to verify. Once you paste or type news headline, then press enter.

5. Once you hit the enter, program will take user input (news headline) and will be used by model to classify in one of categories of "True" and "False". Along with classifying the news headline, model will also provide a probability of truth associated with it.


### Members
Team members of this project include
* Mandar Agashe (magashe2@illinois.edu)
* Nishit K Patel (nkp3@illinois.edu)
* Sachin Rao (sachinr2@illinois.edu)
