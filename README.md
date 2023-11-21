### Executive Summary
Human’s are very complex creatures. We all have our own dialect, and way we string words togethers when we communicate with each other. A question or answer will vary depending on who’s outputting it, even though they may all carry the same message. The introduction of AI has allowed for a new entrant into this space, with AI having that same capability of stringing words together in it’s own form. 

With so much of our world held within the digital space, you can never know who is on the other end of your communication point. You can be talking to someone, and not know whether it is a human or AI generated responses. Such can be a big problem when it comes to certain fields/spaces, as there will be users who will use bots to return AI generated responses and abuse whatever application/program they’re using, or human they are talking too. 

Luckily, there are ways to predict and identify whether or not a given statement reigns from a human or AI. Through the use of NLP (Natural Language Processing), we can build predictive models where given a statement, can predict whether the statement came from a human or AI. Specifically, we can train our model towards a certain user base or group of people with a certain dialect, to even further train the model in a way AI would have much trouble replicating. 

Our team of data scientists has vast knowledge on a variety of models used within the space, more specifically to NLP. That coupled with our niche knowledge of Reddit, and various machine learning techniques will give us plenty of models to run on the vast source of data we’ll be able to scrape up. Extensive and exhaustive in our approach, we continually look and strive to find the best model possible. 

If you’re interested in capturing >93% of AI generated responses given an equal mix of both human and AI entries, we can make it happen. This proposal and accompanied files go more into detail of the process, and thinking of how we were able to execute and build the model we have today. Let’s free Reddit of bots and let the users voice be the only one heard. 

### Legend
- README-old: README included with project
- README: README for the project
- reddit_ai_df.csv: Raw dataframe with all information needed included within
- final_dataframe.csv : Final dataframe with all columns included as prescribed in README-OLD
- real_clean_and_model.ipynb: Cleaning and modelling of final_dataframe
The below files may have a problem running due to missing API keys and path files not being updated (shifted some files around to make more organized)
- reddit_api.ipynb: Gathering of data using reddit API
- real_openai.ipynb: Gathering of data using OpenAI API

ALL OTHER FILES CAN BE IGNORED (Mostly used for practice/trial and error)

### Data Dictionary
- row_id = Row ID
- top_comment = Top comment from Reddit
- answers = Answer from OpenAI
- who_from = Binary classification of Reddit (0) or OpenAI (1)

### Conclusion & Recommendations
- BEST MODEL: Log Regrsesion + TFIDFVectorization while utilizing GridSearch and Lammetization given the following parameters turned out to be best model:
    {'cvec__max_df': 0.5,
     'cvec__max_features': 5000,
     'cvec__min_df': 10,
     'cvec__ngram_range': (1, 2),
     'cvec__stop_words': None}
- Classification Metrics for Best Model:
    - Accuracy = 92.97%
    - Misclassification Rate =	  7.03%
    - Sensitivity = 		91.42%
    - Specificity = 		94.38%
    - Precision = 		93.67%


In conclusion, we were able to build a model which successfuly categorized over 93% of responses to being either human or AI. When building this model, we tried a variety of feature engineering and various machine learning methods. Ultimately, a log regression with lammetization, and TIFIDFVectorization turned out to give us the best scoring model. On our training data, the model scored 0.991 and 0.927 on our test data which shows our model to be overfit, but still performing well with high accuracy. 

Although overfit to the training data, we are confident the model will continue to perform well on unseen data similar to how it did on the testing data. The only caveat would be if the unseen data was taken from sources outside what we used to train our model. People within a given community tend to have similar speech patterns, and that is no different with the Reddit communities to which we pulled our data from. Our model is trained towards that and on the AI side its trained towards the davinci engine used within ChatGPT; any data outside that scope, we expect our model to perform lower on.

With our model, we found it important to minimize false negatives, as we did not want to mark a response as AI when it turned out to be a human. In turn, our sensitivity and accuracy amongst the other classification metrics are what we want to see optimized. By identifying bots, and keeping misclassification of humans for bots as low as possible, we can make it so that most bots are identified, while also allowing all users to not worry about getting flagged. 

Another model we had (which wasn't our best) was using Bernoulli Naive Bayes. Naive Bayes classifier is made specifcally for classification problems, and the Bernoulli Naive Bayes is specifically used for binary classification problems (similar to what we have). We also used CountVectorization for the text, and removed stop words. When we trained the data, we ended up getting a train score of 0.801 and a test score of 0.771. Much less performance loss between the training and test data, however our false positives were horrendous. We had 309 false positives out of 1394 predictions. In our case, false positives meant predicting a response to be from Reddit but it turning out to being from ChatGPT. On the other hand, we only had 5 false negatives. Due to this, our specificty (57.67%) and precision (68.08%) were quite low while our sensitivity (99.25%) was very high. Due to the lower training and test score vs the other model, and the discrpency in balance between classification metrics and false negatives to false positvies, we decided to move on from this model. 

Recommendations we would make to improve our model is firstly to increase our training and testing size; by training on data not just from Reddit, but various forums and websites, you get a variety of dialect and word use in various ways which will only help train the model, to which you can then test it out. Another recomendation would be to build a better model if possible. A model which performs slightly lower on the training data but higher on the testing data would be ideal to counteract some of that overfitting. All else equal, our model still holds its weight and we believe is still highly predictable in classifying whether a response is human or AI generated. 

All in all, our model would work to flag >93% of responses generated by AI, effictevely keeping the human made responses while getting rid of the unwanted ones. As our world continues to become more digitalized, bots which use AI generated responses will continue to grow in size. Our effort to identify and flag these AI generated responses is the first of many iterations to come, and while our current model is highly effective we will continue to collect data and build to make our's the best predictive model for whether a response is made by a human or AI! 


   
### Sources
- Sources for various code is linked within cells that they're refrenced
- Referred back to lessons 2.04-2.06, lab 2.02, breakfast hour on Sep 14 2023 and hackathon notes