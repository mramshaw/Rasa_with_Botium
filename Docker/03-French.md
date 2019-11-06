# French

Using a different language (French)

## Contents

The contents are as follows:

* [Create the project](#create-the-project)
* [Change the configuration](#change-the-configuration)
* [Train the model](#train-the-model)
* [Interact with the bot](#interact-with-the-bot)

## Create the project

Lets start with the default project.

```bash
$ mkdir french
$ chmod 777 french
$ docker run -v $(pwd)/french:/app --name rasa -it --rm mramshaw4docs/rasa:latest-spacy-fr init
Welcome to Rasa! 🤖

To get started quickly, an initial project will be created.
If you need some help, check out the documentation at https://rasa.com/docs/rasa.
Now let's start! 👇🏽

? Please enter a path where the project will be created [default: current directory] .                                                                                                                                                                        
Created project directory at '/app'.
Finished creating project structure.
Training an initial model...
Training Core model...

<...>

2019-11-06 22:34:47 INFO     rasa.nlu.model  - Successfully saved model into '/tmp/tmp2n508owg/nlu'
NLU model training completed.
Your Rasa model is trained and saved at '/app/models/20191106-223437.tar.gz'.
? Do you want to speak to the trained assistant on the command line? 🤖  No                                                                                                                                                                                    
Ok 👍🏼. If you want to speak to the assistant, run 'rasa shell' at any time inside the project directory.
$
```

## Change the configuration

Update [french/config.yml](./french/config.yml), replacing `en` with `fr` and `supervised_embeddings` with `pretrained_embeddings_spacy`.

Also, update [french/domain.yml](./french/domain.yml), [french/data/nlu.yml](./french/data/nlu.yml), and [french/data/stories.yml](./french/data/stories.yml).

## Train the model

Now lets train (okay, retrain) the model:

```bash
$ docker run -v $(pwd)/french:/app --name rasa -it --rm mramshaw4docs/rasa:latest-spacy-fr train
Training Core model...
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 4844.43it/s, # trackers=1]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 1603.20it/s, # trackers=5]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 357.84it/s, # trackers=20]
Processed Story Blocks: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 240.52it/s, # trackers=24]
Processed trackers: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 5/5 [00:00<00:00, 4583.94it/s, # actions=16]
Processed actions: 16it [00:00, 12975.42it/s, # examples=16]
Processed trackers: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 231/231 [00:00<00:00, 1988.34it/s, # actions=126]
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
2019-11-06 23:34:05 INFO     rasa.core.policies.keras_policy  - Fitting model with 126 total samples and a validation split of 0.1
Epoch 1/100
126/126 [==============================] - 0s 3ms/sample - loss: 2.5636 - acc: 0.1587
Epoch 2/100
126/126 [==============================] - 0s 79us/sample - loss: 2.4965 - acc: 0.2540
Epoch 3/100
126/126 [==============================] - 0s 144us/sample - loss: 2.4393 - acc: 0.3730
Epoch 4/100
126/126 [==============================] - 0s 87us/sample - loss: 2.3927 - acc: 0.4206
Epoch 5/100
126/126 [==============================] - 0s 65us/sample - loss: 2.3082 - acc: 0.4365
Epoch 6/100
126/126 [==============================] - 0s 66us/sample - loss: 2.2499 - acc: 0.4524
Epoch 7/100
126/126 [==============================] - 0s 80us/sample - loss: 2.1815 - acc: 0.4603
Epoch 8/100
126/126 [==============================] - 0s 96us/sample - loss: 2.0885 - acc: 0.4603
Epoch 9/100
126/126 [==============================] - 0s 67us/sample - loss: 2.0198 - acc: 0.4603
Epoch 10/100
126/126 [==============================] - 0s 65us/sample - loss: 1.9029 - acc: 0.4603
Epoch 11/100
126/126 [==============================] - 0s 65us/sample - loss: 1.8475 - acc: 0.4603
Epoch 12/100
126/126 [==============================] - 0s 144us/sample - loss: 1.7885 - acc: 0.4603
Epoch 13/100
126/126 [==============================] - 0s 67us/sample - loss: 1.7465 - acc: 0.4603
Epoch 14/100
126/126 [==============================] - 0s 66us/sample - loss: 1.6837 - acc: 0.4603
Epoch 15/100
126/126 [==============================] - 0s 66us/sample - loss: 1.6597 - acc: 0.4603
Epoch 16/100
126/126 [==============================] - 0s 99us/sample - loss: 1.6405 - acc: 0.4603
Epoch 17/100
126/126 [==============================] - 0s 82us/sample - loss: 1.6067 - acc: 0.4603
Epoch 18/100
126/126 [==============================] - 0s 66us/sample - loss: 1.5760 - acc: 0.4603
Epoch 19/100
126/126 [==============================] - 0s 67us/sample - loss: 1.5761 - acc: 0.4603
Epoch 20/100
126/126 [==============================] - 0s 91us/sample - loss: 1.5611 - acc: 0.4603
Epoch 21/100
126/126 [==============================] - 0s 87us/sample - loss: 1.5398 - acc: 0.4603
Epoch 22/100
126/126 [==============================] - 0s 66us/sample - loss: 1.5093 - acc: 0.4603
Epoch 23/100
126/126 [==============================] - 0s 66us/sample - loss: 1.4901 - acc: 0.4603
Epoch 24/100
126/126 [==============================] - 0s 80us/sample - loss: 1.4761 - acc: 0.4603
Epoch 25/100
126/126 [==============================] - 0s 84us/sample - loss: 1.4682 - acc: 0.4603
Epoch 26/100
126/126 [==============================] - 0s 69us/sample - loss: 1.4503 - acc: 0.4603
Epoch 27/100
126/126 [==============================] - 0s 65us/sample - loss: 1.4238 - acc: 0.4841
Epoch 28/100
126/126 [==============================] - 0s 81us/sample - loss: 1.4134 - acc: 0.4762
Epoch 29/100
126/126 [==============================] - 0s 81us/sample - loss: 1.3901 - acc: 0.4841
Epoch 30/100
126/126 [==============================] - 0s 67us/sample - loss: 1.3837 - acc: 0.4841
Epoch 31/100
126/126 [==============================] - 0s 65us/sample - loss: 1.3568 - acc: 0.4683
Epoch 32/100
126/126 [==============================] - 0s 132us/sample - loss: 1.3263 - acc: 0.4762
Epoch 33/100
126/126 [==============================] - 0s 66us/sample - loss: 1.3277 - acc: 0.4762
Epoch 34/100
126/126 [==============================] - 0s 65us/sample - loss: 1.2836 - acc: 0.4762
Epoch 35/100
126/126 [==============================] - 0s 69us/sample - loss: 1.2816 - acc: 0.4841
Epoch 36/100
126/126 [==============================] - 0s 98us/sample - loss: 1.2582 - acc: 0.4762
Epoch 37/100
126/126 [==============================] - 0s 66us/sample - loss: 1.2164 - acc: 0.4683
Epoch 38/100
126/126 [==============================] - 0s 66us/sample - loss: 1.1921 - acc: 0.4841
Epoch 39/100
126/126 [==============================] - 0s 72us/sample - loss: 1.1673 - acc: 0.4841
Epoch 40/100
126/126 [==============================] - 0s 91us/sample - loss: 1.1523 - acc: 0.5079
Epoch 41/100
126/126 [==============================] - 0s 67us/sample - loss: 1.1272 - acc: 0.4841
Epoch 42/100
126/126 [==============================] - 0s 68us/sample - loss: 1.0924 - acc: 0.5714
Epoch 43/100
126/126 [==============================] - 0s 83us/sample - loss: 1.1015 - acc: 0.5397
Epoch 44/100
126/126 [==============================] - 0s 85us/sample - loss: 1.0301 - acc: 0.6270
Epoch 45/100
126/126 [==============================] - 0s 67us/sample - loss: 1.0111 - acc: 0.6667
Epoch 46/100
126/126 [==============================] - 0s 66us/sample - loss: 1.0044 - acc: 0.7143
Epoch 47/100
126/126 [==============================] - 0s 98us/sample - loss: 1.0131 - acc: 0.7302
Epoch 48/100
126/126 [==============================] - 0s 66us/sample - loss: 0.9515 - acc: 0.8095
Epoch 49/100
126/126 [==============================] - 0s 67us/sample - loss: 0.9306 - acc: 0.7857
Epoch 50/100
126/126 [==============================] - 0s 66us/sample - loss: 0.9211 - acc: 0.7698
Epoch 51/100
126/126 [==============================] - 0s 102us/sample - loss: 0.8838 - acc: 0.8175
Epoch 52/100
126/126 [==============================] - 0s 67us/sample - loss: 0.8473 - acc: 0.7937
Epoch 53/100
126/126 [==============================] - 0s 67us/sample - loss: 0.8143 - acc: 0.8333
Epoch 54/100
126/126 [==============================] - 0s 71us/sample - loss: 0.8351 - acc: 0.7857
Epoch 55/100
126/126 [==============================] - 0s 88us/sample - loss: 0.8250 - acc: 0.7857
Epoch 56/100
126/126 [==============================] - 0s 65us/sample - loss: 0.7554 - acc: 0.8730
Epoch 57/100
126/126 [==============================] - 0s 66us/sample - loss: 0.7414 - acc: 0.8651
Epoch 58/100
126/126 [==============================] - 0s 78us/sample - loss: 0.7460 - acc: 0.8254
Epoch 59/100
126/126 [==============================] - 0s 79us/sample - loss: 0.7512 - acc: 0.8333
Epoch 60/100
126/126 [==============================] - 0s 67us/sample - loss: 0.7402 - acc: 0.8492
Epoch 61/100
126/126 [==============================] - 0s 71us/sample - loss: 0.7158 - acc: 0.8571
Epoch 62/100
126/126 [==============================] - 0s 79us/sample - loss: 0.6818 - acc: 0.9048
Epoch 63/100
126/126 [==============================] - 0s 81us/sample - loss: 0.6657 - acc: 0.8889
Epoch 64/100
126/126 [==============================] - 0s 67us/sample - loss: 0.6475 - acc: 0.8651
Epoch 65/100
126/126 [==============================] - 0s 67us/sample - loss: 0.6451 - acc: 0.8810
Epoch 66/100
126/126 [==============================] - 0s 93us/sample - loss: 0.6497 - acc: 0.8571
Epoch 67/100
126/126 [==============================] - 0s 72us/sample - loss: 0.5988 - acc: 0.9206
Epoch 68/100
126/126 [==============================] - 0s 73us/sample - loss: 0.5967 - acc: 0.9048
Epoch 69/100
126/126 [==============================] - 0s 66us/sample - loss: 0.5741 - acc: 0.8889
Epoch 70/100
126/126 [==============================] - 0s 125us/sample - loss: 0.5862 - acc: 0.9127
Epoch 71/100
126/126 [==============================] - 0s 70us/sample - loss: 0.5928 - acc: 0.8730
Epoch 72/100
126/126 [==============================] - 0s 69us/sample - loss: 0.5687 - acc: 0.9127
Epoch 73/100
126/126 [==============================] - 0s 91us/sample - loss: 0.5297 - acc: 0.9365
Epoch 74/100
126/126 [==============================] - 0s 70us/sample - loss: 0.5427 - acc: 0.9127
Epoch 75/100
126/126 [==============================] - 0s 65us/sample - loss: 0.5328 - acc: 0.8810
Epoch 76/100
126/126 [==============================] - 0s 67us/sample - loss: 0.5338 - acc: 0.9206
Epoch 77/100
126/126 [==============================] - 0s 90us/sample - loss: 0.5078 - acc: 0.9206
Epoch 78/100
126/126 [==============================] - 0s 72us/sample - loss: 0.4690 - acc: 0.9365
Epoch 79/100
126/126 [==============================] - 0s 66us/sample - loss: 0.4732 - acc: 0.9444
Epoch 80/100
126/126 [==============================] - 0s 65us/sample - loss: 0.4741 - acc: 0.9444
Epoch 81/100
126/126 [==============================] - 0s 139us/sample - loss: 0.4382 - acc: 0.9524
Epoch 82/100
126/126 [==============================] - 0s 66us/sample - loss: 0.4548 - acc: 0.9524
Epoch 83/100
126/126 [==============================] - 0s 82us/sample - loss: 0.4365 - acc: 0.9444
Epoch 84/100
126/126 [==============================] - 0s 85us/sample - loss: 0.4372 - acc: 0.9365
Epoch 85/100
126/126 [==============================] - 0s 66us/sample - loss: 0.4106 - acc: 0.9365
Epoch 86/100
126/126 [==============================] - 0s 66us/sample - loss: 0.4255 - acc: 0.9365
Epoch 87/100
126/126 [==============================] - 0s 101us/sample - loss: 0.4167 - acc: 0.9365
Epoch 88/100
126/126 [==============================] - 0s 72us/sample - loss: 0.3882 - acc: 0.9683
Epoch 89/100
126/126 [==============================] - 0s 66us/sample - loss: 0.3789 - acc: 0.9603
Epoch 90/100
126/126 [==============================] - 0s 66us/sample - loss: 0.3969 - acc: 0.9365
Epoch 91/100
126/126 [==============================] - 0s 84us/sample - loss: 0.3726 - acc: 0.9603
Epoch 92/100
126/126 [==============================] - 0s 67us/sample - loss: 0.3589 - acc: 0.9444
Epoch 93/100
126/126 [==============================] - 0s 67us/sample - loss: 0.3295 - acc: 0.9762
Epoch 94/100
126/126 [==============================] - 0s 104us/sample - loss: 0.3852 - acc: 0.9365
Epoch 95/100
126/126 [==============================] - 0s 71us/sample - loss: 0.3388 - acc: 0.9762
Epoch 96/100
126/126 [==============================] - 0s 67us/sample - loss: 0.3296 - acc: 0.9683
Epoch 97/100
126/126 [==============================] - 0s 91us/sample - loss: 0.3548 - acc: 0.9444
Epoch 98/100
126/126 [==============================] - 0s 70us/sample - loss: 0.3894 - acc: 0.9206
Epoch 99/100
126/126 [==============================] - 0s 66us/sample - loss: 0.3005 - acc: 0.9683
Epoch 100/100
126/126 [==============================] - 0s 67us/sample - loss: 0.3285 - acc: 0.9524
2019-11-06 23:34:07 INFO     rasa.core.policies.keras_policy  - Done fitting keras policy model
2019-11-06 23:34:08 INFO     rasa.core.agent  - Persisted model to '/tmp/tmp44id2oud/core'
Core model training completed.
Training NLU model...
2019-11-06 23:34:08 INFO     rasa.nlu.utils.spacy_utils  - Trying to load spacy model with name 'fr'
2019-11-06 23:34:25 INFO     rasa.nlu.components  - Added 'SpacyNLP' to component cache. Key 'SpacyNLP-fr'.
2019-11-06 23:34:25 INFO     rasa.nlu.training_data.training_data  - Training data stats: 
	- intent examples: 43 (7 distinct intents)
	- Found intents: 'deny', 'greet', 'mood_great', 'affirm', 'mood_unhappy', 'bot_challenge', 'goodbye'
	- Number of response examples: 0 (0 distinct response)
	- entity examples: 0 (0 distinct entities)
	- found entities: 

2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component SpacyNLP
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component SpacyTokenizer
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component SpacyFeaturizer
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component RegexFeaturizer
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component CRFEntityExtractor
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component EntitySynonymMapper
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Starting to train component SklearnIntentClassifier
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
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Finished training component.
2019-11-06 23:34:25 INFO     rasa.nlu.model  - Successfully saved model into '/tmp/tmp44id2oud/nlu'
NLU model training completed.
Your Rasa model is trained and saved at '/app/models/20191106-233426.tar.gz'.
$
```

## Interact with the bot

And finally, to confirm everything still works as expected, lets see how our new bot deals with perfect data:

```bash
$ docker run -v $(pwd)/french:/app --name rasa -it --rm mramshaw4docs/rasa:latest-spacy-fr shell
2019-11-06 23:37:06 INFO     root  - Connecting to channel 'cmdline' which was specified by the '--connector' argument. Any other channels will be ignored. To connect to all given channels, omit the '--connector' argument.
2019-11-06 23:37:06 INFO     root  - Starting Rasa server on http://localhost:5005
2019-11-06 23:37:26 INFO     rasa.nlu.components  - Added 'SpacyNLP' to component cache. Key 'SpacyNLP-fr'.
Bot loaded. Type a message and press enter (use '/stop' to exit): 
Your input ->  bonsoir                                                                                                                                                                                                                                        
Salut, comment vas tu?
Your input ->  parfait                                                                                                                                                                                                                                        
Super, continuez!
Your input ->  salut                                                                                                                                                                                                                                          
Salut, comment vas tu?
Your input ->  mauvais                                                                                                                                                                                                                                        
Voici quelque chose pour vous remonter le moral:
Image: https://i.imgur.com/nGF1K8f.jpg
Est-ce que cela vous a aidé?
Your input ->  non                                                                                                                                                                                                                                            
Au revoir
Your input ->  /stop                                                                                                                                                                                                                                          
2019-11-06 23:38:44 INFO     root  - Killing Sanic server now.
$
```

The core functionality seems to be fine.
