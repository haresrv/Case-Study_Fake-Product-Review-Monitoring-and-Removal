# Case Study on Fake Product Review Monitoring and Removal #


Sample lines from Dataset Used: ( label1- *Real* label2- *Fake* )  

| DOC_ID | LABEL      | RATING | VERIFIED_PURCHASE | PRODUCT_CATEGORY | PRODUCT_ID | PRODUCT_TITLE                                                  | REVIEW_TITLE             | REVIEW_TEXT                                                                                                                                                                                                                                                                                                         | 
|--------|------------|--------|-------------------|------------------|------------|----------------------------------------------------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| 
| 1      | __label1__ | 4      | N                 | PC               | B00008NG7N | Targus PAUK10U Ultra Mini USB Keypad, Black                    | useful                   | When least you think so, this product will save the day. Just keep it around just in case you need it for something.                                                                                                                                                                                                | 
| 3      | __label1__ | 3      | N                 | Baby             | B000I5UZ1Q | Fisher-Price Papasan Cradle Swing, Starlight                   | doesn't swing very well. | I purchased this swing for my baby. She is 6 months now and has pretty much out grown it. It is very loud and doesn't swing very well. It is beautiful though. I love the colors and it has a lot of settings, but I don't think it was worth the money.                                                            | 
| 4      | __label1__ | 4      | N                 | Office Products  | B003822IRA | Casio MS-80B Standard Function Desktop Calculator              | Great computing!         | I was looking for an inexpensive desk calcolatur and here it is. It works and does everything I need. Only issue is that it tilts slightly to one side so when I hit any keys it rocks a little bit. Not a big deal.                                                                                                | 
| 10522  | __label2__ | 5      | Y                 | Video DVD        | B003QF1N7K | Disneynature: Oceans                                           | Wonderful DVD            | This DVD is awesome. I love the way that it shows all different kinds of life in the Ocean. Especially that of the Dolphins and the Whales. Finding out about the rays, sharks and many other things that live in the ocean is just as impressive. Just amazing. Simply Wonderful.                                  | 
| 10523  | __label2__ | 5      | N                 | Office Products  | B00D7NYKYE | Quartet Chalkboard, 8.5 x 11 Inches, Wood Finish Frame (80214) | Perfect for the Kitchen  | Roughly the size of a notebook paper, this little chalkboard is incredibly handy.  It mounts easily to any surface with the included double sided tape.  We use it in the kitchen for reminders and little notes.  It is very light weight.  The faux wood edges look nice as well.  We're happy with this product. | 



###### Dataset has not been fact checked for correctness. I couldn't find a reliable datasource as filtering fake reviews is a hard task for humans,let alone for machines. ######



Given the nature of task and the fact that it was tougher to find a reliable dataset which is made available for students, I couldn't work on a better
intuitive model.
I found this [repo](https://github.com/anubhavs11/Fake-Product-Review-Monitoring) to be nicer model to begin with. But my use case required usage of 
neural networks to solve this problem. So I went with following three implementations

- [x] [Word2Vec](https://github.com/haresrv/Dustbin/blob/master/2.0-Word2Vec.ipynb)
- [x] [Doc2Vec](https://github.com/haresrv/Dustbin/blob/master/2-Doc2Vec.ipynb)
- [x] [BERT](https://github.com/haresrv/Dustbin/blob/master/3-Keras%20Bert.ipynb)

ROC Curves:


**1. Simple Word2Vec**
<br>

![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/2.1-Word2Vec_Simple_ROC.png)

<br>

**2. Word2Vec concat with meta data**

![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/2.2-Word2Vec_Concat_ROC.png) ![Model Structure](http://digital-thinking.de/wp-content/uploads/2018/07/combine-244x300.png)

<br>

**3. Simple Doc2Vec**
<br>

![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/2-Doc2Vec_ROC.png)![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/2-Doc2Vec_Conf_Matrix.png)

<br>

**4. Simple BERT**
<br>

![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/BERT_ROC.png)![Wor](https://github.com/haresrv/Dustbin/blob/master/Performances/BERT_CONFMATRIX.png)


Inferences:

* Basic BOW and TFIDF won't be suitable for this usecase simply, because reviews generally do contain repeating words and these methods will
give less weightage for words which occur frequently.

* Word2Vec captures the relationship between words through embeddings and using W2V embeddings with LSTM produced a reasonably better model which gave accuracy slightly greater than blind guessing
But model seem to overfit the training set as validation accuracy was fluctuating back and forth

* Doc2Vec was improvement over Word2Vec which works on TaggedSentences to produce slightly complex embeddings. But here also, model seem to overfit the training set as validation accuracy was fluctuating back and forth.

* BERT gave an accuracy of 64% but despite being a complex architecture, it didn't overfit itself, but gave poor predictions on test dataset.

