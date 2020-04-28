# Customer-service-chatbot-using-tweeter-data
Executive summary 
Our project used data extracted from millions of tweets and replies from companies to build a customer service chatbot to automatically reply users’ queries, helping companies deal with customer concerns and improving customer satisfaction. The basic idea is to find requests from customers similar to the one provided as a query and return answers. 

There are two major steps in building the chatbot using a machine learning based approach. The first step was text preprocessing: we cleaned tweet data, removed symbols, and joined the questions and answers into the same row to train the model. We used the tweets posted from and to the three most responsive companies Amazon, Apple and Uber only. The next step was feature extraction and modeling: we designed three classes (Seg, Sentence and SentenceSimilarity) and four algorithms (TFIDF, LSI, LDA, and Word2vec) to build models. The chatbot returns up to five most relevant answers from a library of predefined responses, based on the similarity scores between the input question and similar questions answered by the customer service teams.

Apart from the chatbot, we also applied topic modeling. To better learn customers’ needs, we used LDA to extract 10 topics from customers’ tweets to Amazon. These topics can also reflect users' major concerns. Therefore, we used the most popular terms to generate input questions to evaluate the performance of the four models.

Through the above processes, we got the conclusion that LSI has the best performance to find the most relevant answer within the shortest time so we can apply this model to more companies. We also better understood the problems customers encounter most, companies can find direction to improve their service using this result.


Data Description
In this study, the dataset taken from Kaggle includes 3 million tweets and replies from the biggest brands (e.g. Apple, Amazon, Uber) on Twitter and every conversation has at least one request from a consumer and at least one response from a company.  We have seven columns, which are tweet_id, author_id, inbound, created_at, text, response_tweet_id, and in_response_to_tweet_id. The columns and their explanations are listed in the below table.


Data Preprocessing
Since the model we are building is a retrieval-based chatbot, the basic idea was to encode the customer queries in the dataset and find the most similar questions to the input question. For the data preprocessing part, since the dataset was collected from twitter, we need to get rid of the ‘@’ symbols and the user name in the content to make it more like a conversation between customers and the customer support team, when returning answers from the chatbot. 

This project focused on building the chatbots for Amazon, Apple and Uber only. We grouped the tweets by different companies in order to build chatbots for queries related to different companies. We then paired the questions and the corresponding responses into the same rows. This way allows the chatbot to return the specific answer of the most similar question identified by the model.

Pipeline for Chatbot
We have several classes in the pipeline: 

the class Seg was designed to do the preprocessing of the tweets content, including transition of cases, deleting symbols, tokenization, options between removing the stop words and stemming; 
the class Sentence is a connection between the modeling part and the preprocessing part; 
the class Sentence Similarity is to build the four encoding methods - TFIDF, LSI, LDA, and Word2vec - for calculating the similarity scores. For the Word2vec approach, we manually calculate cosine similarity to get the similarity scores. For the other three approaches, we used the MatrixSimilarity function in Gensim to calculate cosine similarity. This class also allows to return the indexes of the five most similar questions to the input question for the chatbot to find several relevant answers.
The main coding process for building the chatbot included reading data, the interface and the calling of the chatbot. The chatbot is designed to first ask for the one out of four encoding methods, the company that the customer asks for, and then the question needed for a reply. The whole chatting process can be interrupted by entering ‘q’. The threshold of the similarity score to return answers is set to be 0.5. If there are no pairs in the dataset that can give a score higher than the threshold, the robot will ask the user to contact the manual services. 

During the conversation, the robot also asks the user if the returned answers have solved their problems. If not, the robot will return the next most similar answer, which is also supposed to have a score higher than the threshold. At last, the robot will give the top five similar questions and the similarity scores. It also tells us the setup time and the time for running, which are important evaluation metrics. In fact, the robot has a better performance when using stemming but without simply deleting the stop words, after testing for a number of times.

Topic Modelling
To better understand the customers’ queries related to Amazon, for example, the Latent Dirichlet Allocation (LDA) algorithm in the Gensim package was applied to extract 10 topics from customers’ tweets answered by Amazon customer services. Similar but slightly different preprocessing steps were used to clean the text by first removing the '@' symbol, punctuations, stop words including words that appear only once, transforming to lowercase, and tokenization. To generate a Term Document Matrix, a token dictionary class and a corpus were created. 

