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
1. questions contains HTML tag [<code>] tag. So separate out code-snippets from the Body
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

