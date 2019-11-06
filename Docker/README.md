# Docker

Trying out Rasa with Docker

## Contents

The contents are as follows:

* [Verify Prerequisites](#verify-prerequisites)
    * [`docker` and `docker-compose`](#docker-and-docker-compose)
    * [Check for the latest version of Rasa](#check-for-the-latest-version-of-rasa)
    * [Pull the Docker image](#pull-the-docker-image)
* [Create the dafault project](#create-the-default-project)
* [To Do](#to-do)
* [Credits](#credits)

## Verify Prerequisites

Lets verify that we have everything we need to proceed.

#### `docker` and `docker-compose`

Check for `docker` and `docker-compose`:

```bash
$ docker -v && docker-compose -v
Docker version 19.03.4, build 9013bf583a
docker-compose version 1.23.1, build b02f1306
$
```

#### Check for the latest version of Rasa

__1.4.2__ as per http://hub.docker.com/r/rasa/rasa/tags

#### Pull the Docker image

```bash
$ docker pull rasa/rasa:1.4.2
1.4.2: Pulling from rasa/rasa
8d691f585fa8: Pull complete
49bdb6f85638: Pull complete
73c12d19d464: Pull complete
9964ba7bfd8f: Pull complete
18a21a4ca4a0: Pull complete
d9072db337b5: Pull complete
8a377a815e92: Pull complete
dca83e7d804c: Pull complete
5310e3b991c6: Pull complete
e92acf81f819: Pull complete
1fd0e7fa4db2: Pull complete
Digest: sha256:bf70a20e4067c1afda970111c5dd44de0ea86aa3d21809e1b05002a91b9289e6
Status: Downloaded newer image for rasa/rasa:1.4.2
docker.io/rasa/rasa:1.4.2
$
```

## Create the default project

Rasa is supplied with a default project.

For details of creating the [default Rasa project](./01-Default_project.md)

## Use a different pipeline

By default, the `supervised_embeddings` pipeline is used.

There is also a `pretrained_embeddings_spacy` pipeline.

Read about the difference [here](http://rasa.com/docs/rasa/nlu/choosing-a-pipeline/#the-short-answer).

For details of using the [pretrained spaCy embeddings](./02-Pretrained_spaCy_embeddings.md)

## To Do

- [x] Train a Rasa Model
- [ ] Automate the testing of our bot
- [ ] Investigate Rasa's [Training Data Format](http://rasa.com/docs/rasa/nlu/training-data-format/)
- [ ] Investigate Rasa's [Custom Actions](http://rasa.com/docs/rasa/core/actions/#custom-actions)
- [ ] Investigate Rasa's [Pipelines](http://rasa.com/docs/rasa/nlu/choosing-a-pipeline/)
- [ ] Write a custom [Tracker Store](http://rasa.com/docs/rasa/api/tracker-stores/)

## Credits

Running Rasa with Docker:

    http://rasa.com/docs/rasa/user-guide/running-rasa-with-docker/
