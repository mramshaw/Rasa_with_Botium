# Rasa_with_Botium

![Rasa Logo](images/21214473_small.png) ![Botium Logo](images/Botium_logo.png)

Having created a [slackbot with GCP](http://github.com/mramshaw/GCP-Slackbot), [Alexa Skills](http://github.com/mramshaw/Alexa-Stuff), 
and [Google Assistant Apps](http://github.com/mramshaw/Google-Assistant), it seemed to be time to have a look at [Rasa](http://rasa.com/)
and [Botium](http://www.botium.at/).

Rasa and Botium are both Open-Source. Rasa is a general chatbot framework, while Botium is a generic chatbot testing framework.

Both can be added into existing frameworks via external linkages called ___webhooks___.

## Botium

Botium describes itself as "The Selenium for Chatbots".

It offers a number of integrations (which it refers to as "connectors"),
 both for testing Alexa Skills as well as Dialogflow apps.

## Privacy

For my slackbot I used __Wit.ai__ - which is owned by __Facebook__.

For my Alexa Skills I used __Alexa__ - which is owned by __Amazon__.

For my Google Assistant Apps I used __Dialogflow__ - which is owned by __Google__.

For anyone remotely concerned about privacy, being able to track user data and
how it is processed via Open-Source code is definitely worth considering.

## Reference

A selection of useful references follows.

#### Why Rasa

For a good summary of "Why Rasa?" the following article is worth a read:

    http://medium.com/rasa-blog/do-it-yourself-nlp-for-bot-developers-2e2da2817f3d

[The article also has some details on the underpinnings of Rasa.]

And the Rasa Blog version:

    http://blog.rasa.com/do-it-yourself-nlp-for-bot-developers/

[The [Medium.com](http://medium.com/) version also has some interesting comments.]

#### Rasa Docs

The documentation for Rasa may be found here:

    http://rasa.com/docs/

#### Rasa Blog

Some useful articles on Rasa and chatbots can be found on their blog:

    http://blog.rasa.com

#### Botium Blog

Some useful articles on Botium can be found on their blog:

    http://www.botium.at/blog.html

#### Botium testing with BDD

The following article seems to give a good grounding on Botium and BDD:

    http://www.sitepoint.com/bdd-javascript-cucumber-gherkin/

## To Do

- [ ] Investigate Rasa
- [ ] Test Botium Connector for Alexa
- [ ] Test Botium Connector for Dialogflow
- [ ] Investigate [Botium BDD Samples](http://github.com/codeforequity-at/botium-bdd-samples)
