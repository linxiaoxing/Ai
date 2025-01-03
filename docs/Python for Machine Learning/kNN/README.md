K-Nearest Neighbors Algorithm in Practice

This article will start with the k-nearest neighbor (kNN) algorithm started with the idea of ​​​​using Python 3 to write code step by step for practical training. In addition, I also provided the corresponding data set and annotated the code in detail. In addition, this article also explains how sklearn implements the k-nearest neighbor algorithm. Practical examples: movie category classification, dating website pairing effect determination, handwritten digit recognition.

I have prepared very detailed learning materials for you, including the learning route for algorithm engineers and Leetcode practice notes.I hope they can help readers avoid detours:
[How I became an algorithm engineer, a very detailed learning path](https://mp.weixin.qq.com/s/oQHXG2pdJXLQpeBsNQkPDA)


**Introduction to k-nearest neighbor method**

   The k-nearest neighbor (k-NN) method is a basic classification and regression method proposed by Cover T and Hart P in 1967. Its working principle is: there is a sample data set, also known as a training sample set, and each data in the sample set has a label, that is, we know the corresponding relationship between each data in the sample set and its corresponding classification. After inputting new data without labels, each feature of the new data is compared with the features corresponding to the data in the sample set, and then the algorithm extracts the classification label of the most similar data (nearest neighbor) of the sample. Generally speaking, we only select the first k most similar data in the sample data set, which is the origin of k in the k-nearest neighbor algorithm. Usually k is an integer not greater than 20. Finally, select the classification with the most occurrences in the k most similar data as the classification of the new data.

As a simple example, we can use the k-nearest neighbor algorithm to classify whether a movie is a romance or an action movie.

Table 1.1 is the data set we have, that is, the training sample set. This data set has two features, namely the number of fighting scenes and the number of kissing scenes. In addition, we also know the type of each movie, that is, the classification label. With the naked eye, the ones with more kissing scenes are romance movies. The ones with more fighting scenes are action movies. With our many years of experience in watching movies, this classification is reasonable. If you give me a movie now, and you tell me the number of fighting scenes and kissing scenes in this movie. Without telling me the type of this movie, I can judge whether this movie is a romance movie or an action movie based on the information you give me. The k-nearest neighbor algorithm can also do this like us humans, the difference is that our experience is more "awesome", while the k-nearest neighbor algorithm relies on existing data. For example, if you tell me that this movie has 2 fighting scenes and 102 kissing scenes, my experience will tell you that this is a romance movie, and the k-nearest neighbor algorithm will also tell you that this is a romance movie. You tell me that another movie has 49 fight scenes and 51 kiss scenes. My "evil" experience may tell you that this may be a "romantic action movie" because the pictures are too beautiful and I dare not imagine it. But the k-nearest neighbor algorithm will not tell you this, because in its eyes, the movie types are only romantic movies and action movies. It will extract the classification labels of the most similar data (nearest neighbors) in the sample set. The result may be a romantic movie or an action movie, but it will never be a "romantic action movie". Of course, this depends on factors such as the size of the data set and the judgment criteria of the nearest neighbor.

![image](https://github.com/user-attachments/assets/2f808d66-35f4-43e6-a774-098ba189dbe8)

Table 1.1 Number of fighting scenes, kissing scenes and film types in each movie

**Distance Metrics**

We already know that the k-nearest neighbor algorithm compares features and then extracts the classification labels of the data with the most similar features (the nearest neighbors) in the sample set. So, how do we make the comparison? For example, let's take Table 1.1 as an example. How do we determine the category of the movie marked by the red dot? As shown in the figure below.
![image](https://github.com/user-attachments/assets/2cf0ed18-8511-4a72-a141-8b3e6c274af1)


