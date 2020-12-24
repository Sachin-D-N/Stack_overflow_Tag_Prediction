# Stack_overflow_Tag_Prediction

![pic1](https://user-images.githubusercontent.com/67965686/103075204-27142a80-45f1-11eb-8ea6-d9cdd55559d0.jpg)

If you are a software engineer or a programmer you must have used stackoverflow atleast once in your life time. But have you ever wondered how stackoverflow predicts the tags for a given question ? In this blog, I will discuss about stackoverflow tag predictor case study.

<h1> Business Problem </h1>

Stack Overflow is the largest, most trusted online community for developers to learn, share their programming knowledge, and build their careers.

Stack Overflow is something which every programmer use one way or another. Each month, over 50 million developers come to Stack Overflow to learn, share their knowledge, and build their careers. It features questions and answers on a wide range of topics in computer programming. The website serves as a platform for users to ask and answer questions, and, through membership and active participation, to vote questions and answers up or down and edit questions and answers in a fashion similar to a wiki or Digg. As of April 2014 Stack Overflow has over 4,000,000 registered users, and it exceeded 10,000,000 questions in late August 2015. Based on the type of tags assigned to questions, the top eight most discussed topics on the site are: Java, JavaScript, C#, PHP, Android, jQuery, Python and HTML.

Data can Found [Here](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data)

Youtube Explanation about the [problem](https://youtu.be/nNDqbUhtIRg)

For More Info Read Research paper [Here](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tagging-1.pdf)

Github code repo: [stackoverflow tag preditor](https://github.com/Sachin-D-N/Stack_overflow_Tag_Prediction/blob/main/Stack_Overflow_Tag_Predictor/Stack_Overflow_Tag_Predictor.ipynb)

## Problem Statement
Predict the tags ( keywords, topics, summaries), given only the question text and its title.

Read the full problem statement on [kaggle](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/)

# Business Objectives and Constraints
- Predict as many tags as possible with high [precision and recall](https://medium.com/analytics-vidhya/performance-metrics-for-machine-learning-models-80d7666b432e).
- Incorrect tags could impact customer experience on StackOverflow.
- No strict latency constraints.

# Machine Learning Problem

## Data

1. Data contains 4 fields

2. Id - Unique identifier for each question

3. Title - The question’s title

4. Body - The body of the question

5. Tags - The tags associated with the question

Click [here](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data) for more details.

All of the data is in 2 files: Train and Test.<br />
<pre>
<b>Size of Train.csv</b> - 6.75GB<br />
<b>Size of Test.csv</b> - 2GB<br />
<b>Number of rows in Train.csv</b> = 6034195<br />
</pre>
The questions are randomized and contains a mix of verbose text sites as well as sites related to math and programming. The number of questions from each site may vary, and no filtering has been performed on the questions (such as closed questions).<br />
<br />

## Sample Data Point

<pre>
<b>Title</b>:  Implementing Boundary Value Analysis of Software Testing in a C++ program?
<b>Body </b>: <pre><code>
        #include&lt;
        iostream&gt;\n
        #include&lt;
        stdlib.h&gt;\n\n
        using namespace std;\n\n
        int main()\n
        {\n
                 int n,a[n],x,c,u[n],m[n],e[n][4];\n         
                 cout&lt;&lt;"Enter the number of variables";\n         cin&gt;&gt;n;\n\n         
                 cout&lt;&lt;"Enter the Lower, and Upper Limits of the variables";\n         
                 for(int y=1; y&lt;n+1; y++)\n         
                 {\n                 
                    cin&gt;&gt;m[y];\n                 
                    cin&gt;&gt;u[y];\n         
                 }\n         
                 for(x=1; x&lt;n+1; x++)\n         
                 {\n                 
                    a[x] = (m[x] + u[x])/2;\n         
                 }\n         
                 for(int i=1; i&lt;n+1; i++)\n         
                 {\n            
                    for(int l=1; l&lt;=i; l++)\n            
                    {\n                 
                        if(l!=1)\n                 
                        {\n                    
                            cout&lt;&lt;a[l]&lt;&lt;"\\t";\n                 
                        }\n            
                    }\n            
                    for(int j=0; j&lt;4; j++)\n            
                    {\n                
                        cout&lt;&lt;e[i][j];\n                
                        for(int k=0; k&lt;n-(i+1); k++)\n                
                        {\n                    
                            cout&lt;&lt;a[k]&lt;&lt;"\\t";\n               
                        }\n                
                        cout&lt;&lt;"\\n";\n            
                    }\n        
                 }    \n\n        
                 system("PAUSE");\n        
                 return 0;    \n
        }\n
        </code></pre>\n\n
        <p>The answer should come in the form of a table like</p>\n\n
        <p>The output is not coming,can anyone correct the code or tell me what\'s wrong?</p>\n'
<b>Tags </b>: 'c++ c'
</pre>



## Mapping the Business problem to a Machine Learning Problem

It is a multi-label classification problem.

In Multi-label Classification, multiple labels (in this problem its tags) may be assigned to each instance and there is no constraint on how many of the classes the instance can be assigned to. Source: [Wiki](https://en.wikipedia.org/wiki/Multi-label_classification)

Find more about multi-label classification problem [here](https://scikit-learn.org/stable/modules/multiclass.html)

A question on Stackoverflow might be about any of C, Pointers, JAVA, Regex, FileIO and/or memory-management at the same time or none of these.

Performance metric
1. Micro F1 score
2. Macro F1 score

Please read this [blog](https://www.kaggle.com/wiki/HammingLoss) to know more about metrics.

## Exploratory Data Analysis

I have used pandas library to load the data. Please visit My [github](https://github.com/Sachin-D-N/Stack_overflow_Tag_Prediction/blob/main/Stack_Overflow_Tag_Predictor/Stack_Overflow_Tag_Predictor.ipynb) repo to see the full code. I have taken a sample of 200k (2 lakh) data points from Train.csv. Here is a list of major observations from EDA.

1. Number of rows in the database: 200000
2. Number of unique tags: 42048
3. Top 10 important tags: ['.a', '.app', '.asp.net-mvc', '.aspxauth', '.bash-profile', '.class-file', '.cs-file', '.doc', '.drv', '.ds-store']
4. There are total 153 tags which are used more than 10000 times.
5. 14 tags are used more than 100000 times.
6. Most frequent tag (i.e. c#) is used 331505 times.
7. Since some tags occur much more frequenctly than others, Micro-averaged F1-score is the appropriate metric for this probelm.

![Untitled](https://user-images.githubusercontent.com/67965686/103080001-fa651080-45fa-11eb-8f37-cd6db0f742aa.png)

8.Tags Analysis
- Maximum number of tags per question: 5
- Minimum number of tags per question: 1
- Avg. number of tags per question: 2.899440
- Questions with 3 tags appeared more in number 

![Untitled](https://user-images.githubusercontent.com/67965686/103080228-66e00f80-45fb-11eb-94d6-93bec6e53e76.png)

## Most Frequent Tags

![Untitled](https://user-images.githubusercontent.com/67965686/103080377-b6bed680-45fb-11eb-9c51-15f7904f9f35.png)

C# appears most number of times, Java is the second most. Majority of the most frequent tags are programming language. And here is the chart for top 20 tags

![Untitled](https://user-images.githubusercontent.com/67965686/103080511-043b4380-45fc-11eb-8f37-fd3d868c4f5a.png)

- Majority of the most frequent tags are programming language.
- C# is the top most frequent programming language.
- Android, IOS, Linux and windows are among the top most frequent operating systems.

## Cleaning and preprocessing of Questions

###### Due to hardware limitations, I am considering only 200K data points
1. questions contains HTML tag code tag ,So separate out code-snippets from the Body
2. Remove Spcial characters from title and Body (not in code)
3. Remove stop words (Except 'C')
4. Remove HTML Tags
5. Convert all the characters into small letters
6. Use SnowballStemmer to stem the words.
Stemming is the process of reducing a word to its word stem.
For Example: "python" is the stem word for the words ["python" "pythoner", "pythoning","pythoned"]
7. Give more weightage to title: Add title three times to the question. Title contains the information which is more specific to the question and also only after seeing the question title, a user decides whether to look into the question in detail. At least most of the users do this if not all.

### Sample question after preprocessing
![Untitled](https://user-images.githubusercontent.com/67965686/103080852-bbd05580-45fc-11eb-9711-3793e6087d70.png)

## Machine Learning Models
- Total number of questions: 199999
- Total number of tags: 23747

Here we are going to use Problem Transformation(Binary Relevance) method to solve the problem.

### Binary Relevance:
Here we are going to convert multi-label classification problem into multiple single class classification problems.For example if we are having 5 multi-label classification problem, then we need to train 5 single class classification models.

Basically in this method, we treat each label (in our case its tag) as a separate single class classification problem. This technique is simple and is widely used.

Please refer to [analytics vidhya’s blog](https://www.analyticsvidhya.com/blog/2017/08/introduction-to-multi-label-classification/) to know more about the techniques to solve a Multi-Label classification problem.

### Downscaling of data
Coming back to our stackoverflow predictor problem, we need to train 30645 models literally!!! Thats really huge (both in terms of time & speed) for a system with 8GB RAM & i5 processor. So we will sample the number of tags instead considering all of them. But how many tags to be sampled with the minimal information loss ? Plotting ‘percentage of questions covered’ Vs ‘Number of tags’ would help to solve this.

![Untitled](https://user-images.githubusercontent.com/67965686/103085341-6d748400-4607-11eb-8796-0780775ce6d6.png)

#### Observations

1. with 500 tags we are covering 90.446% of questions
2. with 5000 tags we are covering 98.77 % of questions
3. By choosing only 500 tags (2% approximately) of the total 23437 tags we are loosing only 9% of the questions & also training 500 models is reasonable good,So we shall choose 500 tags.

### Train and Test data

If the data had timestamp attached for each of the questions, then splitting data with respect to its temporal nature would have made more sense than splitting data randomly. But since the data is not of temporal nature (i.e., no timestamp), we are splitting data randomly into 80% train set & 20% test set.

![Untitled](https://user-images.githubusercontent.com/67965686/103085636-479baf00-4608-11eb-9a79-6dbb0e3457bd.png)

### Featurizing Text Data with TfIdf vectorizer
There are various ways to featurize text data. I have explained this in my [blog](https://medium.com/analytics-vidhya/amazon-fine-food-reviews-featurization-with-natural-language-processing-a386b0317f56) post. First lets featurize the question data with TfIdf vectorizer. 

![Untitled](https://user-images.githubusercontent.com/67965686/103086742-59cb1c80-460b-11eb-8f2d-7e5d76f8e0d0.png)

### Applying Logistic Regression with OneVsRest Classifier (for tfidf vectorizers

##### Hyper parameter tuning for best alpha

![Untitled](https://user-images.githubusercontent.com/67965686/103086915-ed9ce880-460b-11eb-8adf-4c075cd1bba0.png)

Lets use Logistic Regression algo to train 500 models (500 tags) is nothing but SGDClassifier with Log loss.

![Untitled](https://user-images.githubusercontent.com/67965686/103086981-26d55880-460c-11eb-8f8a-8bd0ab343591.png)

##### Results

- Micro F1-measure: 0.492
- Accuracy: 0.222
- Hamming Loss:0.0029

### OneVsRestClassifier with SVM
Lets use SVM algo to train 500 models. Linear-SVM is nothing but SGDClassifier with loss as hinge. After finding the hyperparameter alpha using GridSearchCV , I found out alpha to be 10**6

![Untitled](https://user-images.githubusercontent.com/67965686/103087310-0c4faf00-460d-11eb-8463-6e10e7a67436.png)

##### Results

- Micro F1-measure: 0.487
- Accuracy: 0.201
- Hamming Loss:0.0031

### Observations
From all the models we used so far, Logistic Regression with TfIdf vectorizer and n_grams=(1,3) performed better than rest of the models. But we have trained the Logistic Regression model with large number of data points, so comparing this model with rest the models, which are trained with lesser data points, will not make sense.

Here is the result of all the models....

![Untitled](https://user-images.githubusercontent.com/67965686/103087484-a7e11f80-460d-11eb-9efd-210baa7b1410.png)

Here we have trained only two linear models. Other models like tree based models will not work well here due to high dimension of data. Linear SVM has high time complexity so training 500 models on linear SVM is not feasible. Hence, SGD classifier is the best choice in our case.

### Problem with complex models like Random Forests or GBDT ?
As you might have noticied, I have taken simplest model like Logistic Regression & Linear SVM to train the model. Here is the two primary main reasons why the complex models were not tried

High dimentional data: since we are converting text to TfIdf or BOW vectors, the dimensions we get are very large in size. And when the dimensions are large, typically Random Forests & GBDT won’t work well.

Too many models to train: We have literally 500 models to train (after downscaling of data). And Logistic Regression is the simplest model one can use & it is comparitively faster. If we start using other models like RBF-SVM or RF, it will take too much time to train the model. For me it took more  time to train Linear SVM, that too after downscaling of data by large margin.

#### Enhancements:

To try with more data points (on a system with 32GB RAM & highend processor)
Featurizing Text Data with Word2Vec: When you try Word2Vec, the dimentionality of data reduces & hence complex models like Random Forests or GBDT might work well.

Try using scikit-multilearn library. Please note that this library doesn’t take sparse matrix as input, you need to give dense matrix as input.So obviously you need to have more RAM to use this library.

Thank you for reading.

