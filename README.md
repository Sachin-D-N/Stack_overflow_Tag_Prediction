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

Click [here](Data contains 4 fields

Id - Unique identifier for each question

Title - The question’s title

Body - The body of the question

Tags - The tags associated with the question

Click [here](https://www.kaggle.com/c/facebook-recruiting-iii-keyword-extraction/data) for more details.
