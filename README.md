# CSE587Lab3 Report
## Author: Haolan Wang
## UBIT: 50248614

## Part1. Understand Apache Spark with Titanic data analysis.

###

## Part2.
### 2.1 Collect and clean data
In this step, we use similar functions in Lab2 to collect data from NYTimes in four topics, which are politics, sports, business and another topic about food as we are supposed to choose another topic. By recognizing the key words in the URL of each articles, we could easily get the article into the correct category.  
</br>  And then by using regularization on the data we collected articles, we could get the cleaned data with only words.

#### ![p1](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture1.jpg)
#### ![p2](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture2.jpg)
After collecting the data, I upload them onto AWS s3 bucket to store them for further use.

### 2.2 Feature Engineering

Before the process of feature engineering, we have to do some preprocess to upload the original data we stored in AWS s3. Firstly, do a loop to upload the text files. Secondly, change the text into lower case and create labels using their file names. And then set the scheme, in order to combine the text and labels together and also set the percentage of train and test dataset for further process.

#### ![p3](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture3.jpg)
Reference: https://spark.apache.org/docs/latest/sql-programming-guide.html#inferring-the-schema-using-reflection

</br> In this part, we are going to use spark pipeline to do the feature extraction. And in spark, there several functions designed to complete these tasks. Firstly, we use the tokenizer function and this could help transform the input text, which are collected by step1, into separated words. As shown below. 

#### ![p4](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture4.jpg)
In my implementation, I just need to change sentence into text. 
</br> After extracting individual words from the text, then what I have to do is to make the words more “meaningful”, which means to get rid if those stop words, like I, the, a, etc. This could be accomplished by function remover(). This function could get input filtered and generated filtered output without stop words.

#### ![p5](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture5.jpg)

Then, I apply HashingTF and IDF on the data, which could generate the term frequency vectors and produces IDFmodel, which could help rescale the feature vectors in order the improve the performance.

#### ![p6](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture6.jpg)

## 2.3 Multiclass Classification

Due to that I am using the pipeline provided by spark, I could easily apply the algorithms like Naïve Bayesian and Neural Network into the pipeline and implement the classification process.
</br> And then using the evaluator function to get to know the accuracy of both two methods.

#### ![p7](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture8.png)

And we could observe that they both got quite high accuracy after the training process.

## 2.4 Testing

They we randomly chooses a set of data which contains 50 test files to be applied into the programme and generates the accuracy result.

#### ![p8](https://github.com/HaolanWang/CSE587Lab3/blob/master/Picture9.png)

And we could notice that although that the accuracy are not compatiable with the result in 2.3, the accuracy are still at a quite high level.
