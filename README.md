<img src="https://bit.ly/2VnXWr2" alt="Ironhack Logo" width="100"/>

# Natural Language Processing to predict Myers-Briggs Personality Type
*Miguel García Melgar*

*Data Analytics Part-Time, Barcelona, Dec19 *

## Content
- [Project Description](#project-description)
- [Objective](#objective)
- [Dataset](#dataset)
- [Workflow](#workflow)
  * [Exploratory Data Analysis](#exploratory-data-analysis)
  * [Preprocessing](#preprocessing)
  * [Model Training and Evaluation](#model-training-and-evaluation)
  * [Conclusion](#conclusion)
- [Future Work](#future-work)
- [Tools and requirements](#tools-and-requirements)
- [References](#references)

## Project Description
In order to learn more on NLP while applaying its methods to psychological variables I have been working on this dataset from Kaggle, [(MBTI) Myers-Briggs Personality Type Dataset](https://www.kaggle.com/datasnaek/mbti-type) which holds information on a forum's users' posts and personalities using MBTI.

## Objective
The IT labour market is getting more and more competitive, as there is more demmand than offer of proffesionals. And of course, eveywane wants the best of the best for their company.

Finding the best talent and ensuring they culturally fit in their organizations means a lot of time, effort and money to invest in material, softwere and personality, intelligence and competency measures for Recruitment Teams; even when they have increasingly amount sof candidates' information.

I want to shorten recruitment times and costs in psichometric tests.

So starting with personality tests I pretend to train a model to use text we get from candidates (social networks, cover letters, CV, etc).

To sum up, in this project I want to train a **classification model using text data features and meta-features from each user comments, messages and posts to predict their personalities**.

## Dataset
I have been working on this dataset from Kaggle, [(MBTI) Myers-Briggs Personality Type Dataset](https://www.kaggle.com/datasnaek/mbti-type), that holds data collected through the [PersonalityCafe forum](http://personalitycafe.com/forum/), as it provides a large selection of people and their MBTI personality type, as well as what they have written. So I was working with only two variables, both of them being categorical, `type`(personality type code and my target) and `posts` (50 latest posts of each user).

## Workflow
### Exploratory Data Analysis
First off all I checked how the data looked like as well as it's shape, columns and dtypes. Then I confirmed there where no nulls or duplicates.

<img src="images/output_images/mbti_count.png" align="middle">

When I checked for unique values and target distribution i found out that in posts there was a unique value per entrance, and tha tthe distribution was horribly unbalanced, specially considering distribuitions found by the original researchers and authors of this psychometric measure (MBTI).

<img src="images/mbti_distr_spain.PNG" align="middle">

Finally I created a Bag of Words by tokenizing posts column using Spacy, so as to use them to create a wordcloud and visualize text before starting cleaning it.

<img src="images/output_images/mbti_token_cloud.png" align="middle">

### Preprocessing
* I used SpaCy to clean and lemmatise the words from each post.
* Once cleaned I transformed the corpus of the text to a matrix using TfidfVectorizer.
* As the sparse matrix was quite big I tried on 3 different ways to reduce its dimensionality:
  * Using Truncated SVD with 100 componets.
  * Using UMAP.
  * Using Truncated SVD and then UMAP on its results.
* Enclosing preprocessing, I encoded my target labels i two different ways. One would use all 16 types, and the other would rather focus on its 4 axes. Thereafter, I created 6 different datasets that I will use to train the models by combining each dimensionality reduction strategy which each kind of labeling the target variable. 

### Model Training and Evaluation
#### Machine Learning Models
From the 6 datasets mentioned above, I trained quite a few models by combining different algorithms for each dataset, and each target, but also with the original dataset size and also with resampled versions:
* The algorithms used were `GaussianNB`, `LogisticRegression`, `KNeighborsClassifier`, `DecisionTreeClassifier`, `RandomForestClassifier`, `GradientBoostingClassifier` and `MLPClassifier`.
* So using 7 models, 2 sample sizes, 5 different labels (type + 4 possible dimensions) and 3 dimensionality reduction methods, I ended up training 210 different models. 

<img src="https://github.com/mikongame/NLP-to-predict-Myers-Briggs-Personality-Type/blob/master/images/Model_TSVD_Types.PNG?raw=true" align="middle">

* The table show the results of training the different algorithms with the results from applying TSVD (100 components) to reduce the dimensionality of the types' dataset without resampling, as the best results were obtained from GraddientBoostingClassiffier using this particular sample.
#### Deep Learning Models

#### Fine tuning of the best model

### Conclusion

The model tarined has an F1 Score of 0.651957, that is the model is able to predict MBTI personality type 65,2% of times.

Despite not seeming particularly outstanding results, as a multiclass classification (16 types), randomness baseline was located at 6.25%. So predictions from this model would be more than 10 times more accurate than guessing.

## Future Improvements
Future improvements would include further hyperparameter tuning, trining the best couple of models using better balanced samples and  testing the resulting best model on a completely differente sample.  

Ideally, I would also like to adapt it to Big Five model, as is the personality models of highest predictive validity. Still, adapting it/ doing a new similar model for predicting other psychological metrics out of text would be mesmerizing too.


## Tools and requirements
In order to train more models simultaneously I've been both using Jupyter Notebooks thorught my own machine and also using default virtual machines throught Google Colab.

I have also used the latest Conda  with the last version of the following packages and libraries:
* os
* pandas
* numpy
* scipy
* math
* random
* seaborn
* matplotlib
* PIL
* wordcloud
* re
* itertools
* spacy
* en_core_web_sm
* string
* collections
* pickle
* umap-learn
* yellowbrick
* sklearn 
* keras

## Links
[Repository](https://github.com/mikongame/NLP-to-predict-Myers-Briggs-Personality-Type)  
[Slides](https://drive.google.com/file/d/1rZ-PFzKa57yAYabTOZBMwIlvb0hK7zHN/view?usp=sharing)  
