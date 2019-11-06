# Pretrained spaCy embeddings

Using the pretrained spaCy embeddings

## Contents

The contents are as follows:

* [Create the project](#create-the-project)
* [Change the configuration](#change-the-configuration)
* [Pull the Docker image](#pull-the-docker-image)
* [Train the model](#train-the-model)
* [Compare it with the default project](#compare-it-with-the-default-project)
* [Interact with the bot](#interact-with-the-bot)

## Create the project

Lets start with the default project.

```bash
$ mkdir spaCy
$ chmod 777 spaCy
$ docker run -v $(pwd)/spaCy:/app --name rasa -it --rm rasa/rasa:1.4.2 init
Welcome to Rasa! 🤖

To get started quickly, an initial project will be created.
If you need some help, check out the documentation at https://rasa.com/docs/rasa.
Now let's start! 👇🏽

? Please enter a path where the project will be created [default: current directory] .                                                                                                                                                                        
Created project directory at '/app'.
Finished creating project structure.
Training an initial model...

<...>

NLU model training completed.
Your Rasa model is trained and saved at '/app/models/20191106-201715.tar.gz'.
? Do you want to speak to the trained assistant on the command line? 🤖  No                                                                                                                                                                                    
Ok 👍🏼. If you want to speak to the assistant, run 'rasa shell' at any time inside the project directory.
$
```

Annoyingly, it insists on training this model.

## Change the configuration

Update [spaCy/config.yml](./spaCy/config.yml), replacing `supervised_embeddings` with `pretrained_embeddings_spacy`.

## Pull the Docker image

In order to use spaCy, we will need to pull the appropriate Docker image:

```bash
$ docker pull rasa/rasa:1.4.2-spacy-en
1.4.2-spacy-en: Pulling from rasa/rasa
8d691f585fa8: Already exists 
49bdb6f85638: Already exists 
73c12d19d464: Already exists 
9964ba7bfd8f: Already exists 
18a21a4ca4a0: Already exists 
b548ae0698b0: Pull complete 
d572a93b3447: Pull complete 
c3c2b85892d9: Pull complete 
9ac25f02a1e3: Pull complete 
df8229ae0115: Pull complete 
b39d75616f79: Pull complete 
656d167c4380: Pull complete 
Digest: sha256:762ecc523d524159d204df110d86e9a0c1b30fba7a9e520c484f7849e006f37c
Status: Downloaded newer image for rasa/rasa:1.4.2-spacy-en
docker.io/rasa/rasa:1.4.2-spacy-en
$ 
```

## Train the model

Now lets train (okay, retrain) the model:

```bash
$ docker run -v $(pwd)/spaCy:/app --name rasa -it --rm rasa/rasa:1.4.2-spacy-en train
Training Core model...
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 5221.99it/s, # trackers=1]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 1549.77it/s, # trackers=5]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 363.24it/s, # trackers=20]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 243.11it/s, # trackers=24]
Processed trackers: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 4678.01it/s, # actions=16]
Processed actions: 16it [00:00, 13834.03it/s, # examples=16]
Processed trackers: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 231/231 [00:00<00:00, 1998.89it/s, # actions=126]
Model: "sequential"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
masking (Masking)            (None, 5, 21)             0         
_________________________________________________________________
lstm (LSTM)                  (None, 32)                6912      
_________________________________________________________________
dense (Dense)                (None, 14)                462       
_________________________________________________________________
activation (Activation)      (None, 14)                0         
=================================================================
Total params: 7,374
Trainable params: 7,374
Non-trainable params: 0
_________________________________________________________________
2019-11-06 20:56:06 INFO     rasa.core.policies.keras_policy  - Fitting model with 126 total samples and a validation split of 0.1
Epoch 1/100
126/126 [==============================] - 0s 3ms/sample - loss: 2.5973 - acc: 0.0476
Epoch 2/100
126/126 [==============================] - 0s 83us/sample - loss: 2.5268 - acc: 0.3175
Epoch 3/100
126/126 [==============================] - 0s 71us/sample - loss: 2.4681 - acc: 0.4365
Epoch 4/100
126/126 [==============================] - 0s 83us/sample - loss: 2.4198 - acc: 0.4444
Epoch 5/100
126/126 [==============================] - 0s 71us/sample - loss: 2.3647 - acc: 0.4444
Epoch 6/100
126/126 [==============================] - 0s 67us/sample - loss: 2.2920 - acc: 0.4444
Epoch 7/100
126/126 [==============================] - 0s 68us/sample - loss: 2.2029 - acc: 0.4603
Epoch 8/100
126/126 [==============================] - 0s 77us/sample - loss: 2.1089 - acc: 0.4603
Epoch 9/100
126/126 [==============================] - 0s 71us/sample - loss: 2.0216 - acc: 0.4524
Epoch 10/100
126/126 [==============================] - 0s 70us/sample - loss: 1.9318 - acc: 0.4603
Epoch 11/100
126/126 [==============================] - 0s 70us/sample - loss: 1.8561 - acc: 0.4603
Epoch 12/100
126/126 [==============================] - 0s 95us/sample - loss: 1.7989 - acc: 0.4603
Epoch 13/100
126/126 [==============================] - 0s 69us/sample - loss: 1.7734 - acc: 0.4603
Epoch 14/100
126/126 [==============================] - 0s 68us/sample - loss: 1.7395 - acc: 0.4603
Epoch 15/100
126/126 [==============================] - 0s 67us/sample - loss: 1.6930 - acc: 0.4603
Epoch 16/100
126/126 [==============================] - 0s 74us/sample - loss: 1.6705 - acc: 0.4603
Epoch 17/100
126/126 [==============================] - 0s 76us/sample - loss: 1.6381 - acc: 0.4603
Epoch 18/100
126/126 [==============================] - 0s 67us/sample - loss: 1.6360 - acc: 0.4603
Epoch 19/100
126/126 [==============================] - 0s 67us/sample - loss: 1.5949 - acc: 0.4603
Epoch 20/100
126/126 [==============================] - 0s 87us/sample - loss: 1.5746 - acc: 0.4603
Epoch 21/100
126/126 [==============================] - 0s 77us/sample - loss: 1.5746 - acc: 0.4603
Epoch 22/100
126/126 [==============================] - 0s 68us/sample - loss: 1.5449 - acc: 0.4603
Epoch 23/100
126/126 [==============================] - 0s 67us/sample - loss: 1.5289 - acc: 0.4603
Epoch 24/100
126/126 [==============================] - 0s 89us/sample - loss: 1.5271 - acc: 0.4603
Epoch 25/100
126/126 [==============================] - 0s 75us/sample - loss: 1.4951 - acc: 0.4603
Epoch 26/100
126/126 [==============================] - 0s 68us/sample - loss: 1.4959 - acc: 0.4603
Epoch 27/100
126/126 [==============================] - 0s 65us/sample - loss: 1.4619 - acc: 0.4603
Epoch 28/100
126/126 [==============================] - 0s 100us/sample - loss: 1.4688 - acc: 0.4762
Epoch 29/100
126/126 [==============================] - 0s 70us/sample - loss: 1.4520 - acc: 0.4683
Epoch 30/100
126/126 [==============================] - 0s 67us/sample - loss: 1.4312 - acc: 0.4841
Epoch 31/100
126/126 [==============================] - 0s 70us/sample - loss: 1.3952 - acc: 0.4841
Epoch 32/100
126/126 [==============================] - 0s 96us/sample - loss: 1.3822 - acc: 0.4841
Epoch 33/100
126/126 [==============================] - 0s 69us/sample - loss: 1.3835 - acc: 0.4841
Epoch 34/100
126/126 [==============================] - 0s 66us/sample - loss: 1.3494 - acc: 0.4762
Epoch 35/100
126/126 [==============================] - 0s 74us/sample - loss: 1.3263 - acc: 0.4683
Epoch 36/100
126/126 [==============================] - 0s 83us/sample - loss: 1.3199 - acc: 0.4762
Epoch 37/100
126/126 [==============================] - 0s 67us/sample - loss: 1.3089 - acc: 0.4841
Epoch 38/100
126/126 [==============================] - 0s 67us/sample - loss: 1.2893 - acc: 0.4841
Epoch 39/100
126/126 [==============================] - 0s 84us/sample - loss: 1.2753 - acc: 0.4841
Epoch 40/100
126/126 [==============================] - 0s 77us/sample - loss: 1.2570 - acc: 0.4762
Epoch 41/100
126/126 [==============================] - 0s 70us/sample - loss: 1.2296 - acc: 0.4921
Epoch 42/100
126/126 [==============================] - 0s 68us/sample - loss: 1.2443 - acc: 0.4921
Epoch 43/100
126/126 [==============================] - 0s 93us/sample - loss: 1.1997 - acc: 0.5000
Epoch 44/100
126/126 [==============================] - 0s 76us/sample - loss: 1.2050 - acc: 0.5159
Epoch 45/100
126/126 [==============================] - 0s 68us/sample - loss: 1.1822 - acc: 0.4921
Epoch 46/100
126/126 [==============================] - 0s 67us/sample - loss: 1.1699 - acc: 0.5079
Epoch 47/100
126/126 [==============================] - 0s 126us/sample - loss: 1.1560 - acc: 0.5079
Epoch 48/100
126/126 [==============================] - 0s 67us/sample - loss: 1.1497 - acc: 0.5079
Epoch 49/100
126/126 [==============================] - 0s 66us/sample - loss: 1.1241 - acc: 0.5159
Epoch 50/100
126/126 [==============================] - 0s 88us/sample - loss: 1.0946 - acc: 0.5079
Epoch 51/100
126/126 [==============================] - 0s 74us/sample - loss: 1.0986 - acc: 0.4921
Epoch 52/100
126/126 [==============================] - 0s 68us/sample - loss: 1.0469 - acc: 0.5476
Epoch 53/100
126/126 [==============================] - 0s 66us/sample - loss: 1.0419 - acc: 0.5556
Epoch 54/100
126/126 [==============================] - 0s 123us/sample - loss: 1.0283 - acc: 0.5794
Epoch 55/100
126/126 [==============================] - 0s 70us/sample - loss: 1.0439 - acc: 0.5794
Epoch 56/100
126/126 [==============================] - 0s 66us/sample - loss: 0.9778 - acc: 0.6508
Epoch 57/100
126/126 [==============================] - 0s 89us/sample - loss: 1.0042 - acc: 0.6270
Epoch 58/100
126/126 [==============================] - 0s 77us/sample - loss: 0.9264 - acc: 0.7222
Epoch 59/100
126/126 [==============================] - 0s 74us/sample - loss: 0.9301 - acc: 0.7143
Epoch 60/100
126/126 [==============================] - 0s 69us/sample - loss: 0.8937 - acc: 0.6905
Epoch 61/100
126/126 [==============================] - 0s 84us/sample - loss: 0.8973 - acc: 0.7222
Epoch 62/100
126/126 [==============================] - 0s 69us/sample - loss: 0.8886 - acc: 0.7381
Epoch 63/100
126/126 [==============================] - 0s 68us/sample - loss: 0.8784 - acc: 0.7937
Epoch 64/100
126/126 [==============================] - 0s 74us/sample - loss: 0.8338 - acc: 0.8333
Epoch 65/100
126/126 [==============================] - 0s 76us/sample - loss: 0.8299 - acc: 0.8492
Epoch 66/100
126/126 [==============================] - 0s 67us/sample - loss: 0.8099 - acc: 0.8254
Epoch 67/100
126/126 [==============================] - 0s 67us/sample - loss: 0.7804 - acc: 0.8333
Epoch 68/100
126/126 [==============================] - 0s 106us/sample - loss: 0.7785 - acc: 0.8492
Epoch 69/100
126/126 [==============================] - 0s 69us/sample - loss: 0.7761 - acc: 0.8730
Epoch 70/100
126/126 [==============================] - 0s 68us/sample - loss: 0.7367 - acc: 0.8730
Epoch 71/100
126/126 [==============================] - 0s 76us/sample - loss: 0.7387 - acc: 0.8730
Epoch 72/100
126/126 [==============================] - 0s 68us/sample - loss: 0.7031 - acc: 0.8492
Epoch 73/100
126/126 [==============================] - 0s 81us/sample - loss: 0.7041 - acc: 0.9048
Epoch 74/100
126/126 [==============================] - 0s 66us/sample - loss: 0.7288 - acc: 0.8492
Epoch 75/100
126/126 [==============================] - 0s 90us/sample - loss: 0.6382 - acc: 0.9603
Epoch 76/100
126/126 [==============================] - 0s 69us/sample - loss: 0.6504 - acc: 0.8968
Epoch 77/100
126/126 [==============================] - 0s 69us/sample - loss: 0.6074 - acc: 0.9762
Epoch 78/100
126/126 [==============================] - 0s 87us/sample - loss: 0.6442 - acc: 0.9127
Epoch 79/100
126/126 [==============================] - 0s 69us/sample - loss: 0.6129 - acc: 0.9206
Epoch 80/100
126/126 [==============================] - 0s 65us/sample - loss: 0.5992 - acc: 0.9365
Epoch 81/100
126/126 [==============================] - 0s 69us/sample - loss: 0.5695 - acc: 0.9365
Epoch 82/100
126/126 [==============================] - 0s 82us/sample - loss: 0.5766 - acc: 0.9365
Epoch 83/100
126/126 [==============================] - 0s 66us/sample - loss: 0.5607 - acc: 0.9444
Epoch 84/100
126/126 [==============================] - 0s 67us/sample - loss: 0.5358 - acc: 0.9524
Epoch 85/100
126/126 [==============================] - 0s 97us/sample - loss: 0.5417 - acc: 0.9365
Epoch 86/100
126/126 [==============================] - 0s 72us/sample - loss: 0.5211 - acc: 0.9365
Epoch 87/100
126/126 [==============================] - 0s 67us/sample - loss: 0.5252 - acc: 0.9444
Epoch 88/100
126/126 [==============================] - 0s 72us/sample - loss: 0.5416 - acc: 0.9444
Epoch 89/100
126/126 [==============================] - 0s 84us/sample - loss: 0.5173 - acc: 0.9206
Epoch 90/100
126/126 [==============================] - 0s 68us/sample - loss: 0.5261 - acc: 0.9206
Epoch 91/100
126/126 [==============================] - 0s 68us/sample - loss: 0.4890 - acc: 0.9524
Epoch 92/100
126/126 [==============================] - 0s 101us/sample - loss: 0.4974 - acc: 0.9524
Epoch 93/100
126/126 [==============================] - 0s 71us/sample - loss: 0.4843 - acc: 0.9603
Epoch 94/100
126/126 [==============================] - 0s 69us/sample - loss: 0.4728 - acc: 0.9524
Epoch 95/100
126/126 [==============================] - 0s 86us/sample - loss: 0.5009 - acc: 0.9603
Epoch 96/100
126/126 [==============================] - 0s 68us/sample - loss: 0.4406 - acc: 0.9524
Epoch 97/100
126/126 [==============================] - 0s 69us/sample - loss: 0.4101 - acc: 0.9603
Epoch 98/100
126/126 [==============================] - 0s 67us/sample - loss: 0.4407 - acc: 0.9683
Epoch 99/100
126/126 [==============================] - 0s 80us/sample - loss: 0.4026 - acc: 0.9762
Epoch 100/100
126/126 [==============================] - 0s 69us/sample - loss: 0.4047 - acc: 0.9524
2019-11-06 20:56:09 INFO     rasa.core.policies.keras_policy  - Done fitting keras policy model
2019-11-06 20:56:09 INFO     rasa.core.agent  - Persisted model to '/tmp/tmp_wmuabb6/core'
Core model training completed.
Training NLU model...
2019-11-06 20:56:09 INFO     rasa.nlu.utils.spacy_utils  - Trying to load spacy model with name 'en'
2019-11-06 20:56:23 INFO     rasa.nlu.components  - Added 'SpacyNLP' to component cache. Key 'SpacyNLP-en'.
2019-11-06 20:56:23 INFO     rasa.nlu.training_data.training_data  - Training data stats: 
	- intent examples: 43 (7 distinct intents)
	- Found intents: 'bot_challenge', 'mood_unhappy', 'greet', 'mood_great', 'affirm', 'goodbye', 'deny'
	- Number of response examples: 0 (0 distinct response)
	- entity examples: 0 (0 distinct entities)
	- found entities: 

2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component SpacyNLP
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component SpacyTokenizer
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component SpacyFeaturizer
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component RegexFeaturizer
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component CRFEntityExtractor
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component EntitySynonymMapper
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Starting to train component SklearnIntentClassifier
Fitting 2 folds for each of 6 candidates, totalling 12 fits
[Parallel(n_jobs=1)]: Using backend SequentialBackend with 1 concurrent workers.
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
/build/lib/python3.6/site-packages/sklearn/metrics/classification.py:1143: UndefinedMetricWarning: F-score is ill-defined and being set to 0.0 in labels with no predicted samples.
  'precision', 'predicted', average, warn_for)
[Parallel(n_jobs=1)]: Done  12 out of  12 | elapsed:    0.0s finished
/build/lib/python3.6/site-packages/sklearn/model_selection/_search.py:841: DeprecationWarning: The default of the `iid` parameter will change from True to False in version 0.22 and will be removed in 0.24. This will change numeric results when test-set sizes are unequal.
  DeprecationWarning)
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 20:56:23 INFO     rasa.nlu.model  - Successfully saved model into '/tmp/tmp_wmuabb6/nlu'
NLU model training completed.
Your Rasa model is trained and saved at '/app/models/20191106-205623.tar.gz'.
$
```

## Compare it with the default project

The results from the [default project](./01-Default_project.md) were as follows:

```bash
2019-10-28 20:14:11 INFO     rasa.core.policies.keras_policy  - Done fitting keras policy model
2019-10-28 20:14:11 INFO     rasa.core.agent  - Persisted model to '/tmp/tmpzb41eyv7/core'
Core model training completed.
Training NLU model...
2019-10-28 20:14:11 INFO     rasa.nlu.training_data.training_data  - Training data stats:
	- intent examples: 43 (7 distinct intents)
	- Found intents: 'goodbye', 'greet', 'mood_unhappy', 'mood_great', 'affirm', 'deny', 'bot_challenge'
	- Number of response examples: 0 (0 distinct response)
	- entity examples: 0 (0 distinct entities)
	- found entities:

2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component WhitespaceTokenizer
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component RegexFeaturizer
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component CRFEntityExtractor
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component EntitySynonymMapper
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component CountVectorsFeaturizer
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component CountVectorsFeaturizer
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:11 INFO     rasa.nlu.model  - Starting to train component EmbeddingIntentClassifier
Epochs: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 300/300 [00:02<00:00, 145.34it/s, loss=0.464, acc=1.000]
2019-10-28 20:14:15 INFO     rasa.utils.train_utils  - Finished training embedding policy, train loss=0.464, train accuracy=1.000
2019-10-28 20:14:15 INFO     rasa.nlu.model  - Finished training component.
2019-10-28 20:14:15 INFO     rasa.nlu.model  - Successfully saved model into '/tmp/tmpzb41eyv7/nlu'
NLU model training completed.
Your Rasa model is trained and saved at '/app/models/20191028-201405.tar.gz'.
If you want to speak to the assistant, run 'rasa shell' at any time inside the project directory.
$
```

Hmm, cannot really compare them, it seems to be apples versus oranges ...

## Interact with the bot

And finally, to confirm everything still works as expected, lets see how our new bot deals with (the same) imperfect data:

```bash
$ docker run -v $(pwd)/spaCy:/app --name rasa -it --rm rasa/rasa:1.4.2-spacy-en shell
2019-11-06 21:01:54 INFO     root  - Connecting to channel 'cmdline' which was specified by the '--connector' argument. Any other channels will be ignored. To connect to all given channels, omit the '--connector' argument.
2019-11-06 21:01:54 INFO     root  - Starting Rasa server on http://localhost:5005
2019-11-06 21:02:11 INFO     rasa.nlu.components  - Added 'SpacyNLP' to component cache. Key 'SpacyNLP-en'.
Bot loaded. Type a message and press enter (use '/stop' to exit): 
Your input ->  heya                                                                                                                                                                                                                                           
Hey! How are you?
Your input ->  drizzly                                                                                                                                                                                                                                        
Great, carry on!
Your input ->  heya                                                                                                                                                                                                                                           
Great, carry on!
Your input ->  unhappy                                                                                                                                                                                                                                        
Here is something to cheer you up:
Image: https://i.imgur.com/nGF1K8f.jpg
Did that help you?
Your input ->  Grr!                                                                                                                                                                                                                                           
Bye
Your input ->  /stop                                                                                                                                                                                                                                          
2019-11-06 21:03:35 INFO     root  - Killing Sanic server now.
$
```

Somewhat different than with our default project ... still, the core functionality seems to be fine.
