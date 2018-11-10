# Notes from empnlp 2018

## Graph Formalisms for Meaning Representations (tutorial)

TBD

## Writing Code for NLP Research (tutorial)

TBD

## Standardized Tests as benchmarks for Artificial Intelligence (tutorial)

TBD

## Deep Chit-Chat: Deep Learning for ChatBots (tutorial)

TBD

## User Trait Expression and Portrayal through Social Media (invited talk)

TBD

## Truth or Lie? Spoken Indicators of Deception in Speech (keynote talk)

TBD

## Semantics I (section)

TBD

## Language models (section)

TBD

## IR / text mining (section)

TBD

##  Semantics V (section)

TBD

## NER (section)

TBD

## Sentiment analysis I (section)

### CARER: Contextualized Affect Representations for Emotion Recognition.

http://aclweb.org/anthology/D18-1404

Detect emotions

Twitter analysis

BOW, embeddings

Graph-based patterns (proposed): thanks \*, for \* etc

Wildcards are good for representing structure, but they don't have semantics

Additional step for filling patterns using clustering

Clusters from word2vec can be not sematically representative (good/bad etc)

Used pretrained word2vec, where this problem was resolved

Used CNN for input

refine process

state-of-the-art: FastText, EmoNet, CNN with pretrained embeddings, DeepMoji

### Adversarial Deep Averaging Networks for Cross-Lingual Sentiment Classification

http://emnlp2018.org/downloads/tacl-papers/EMNLP-TACL04.pdf

TreeLSTM, DAN, DRecNN

Most data available in English

Cross lingual classification

Before people used parallel corporas/machinal translation

Low resource languages can not have parallel corporas

Learn language-invariant features

build bilingual word embeddings

Joint feature extractor, sentiment classifier

Naive way (use features as is) doesn't work - features distribution is diffirent

One more loss to force language independent features requires parallel corporas

Language descriminator, adversarial search

If we can't classify the language - we build language-independent features

Use word embeddings, because different languages can really don't share words

Pre-trained bilingual word embeddings, it's possible to train it in fully unsupervised way

Deep averaging network - embeddings average

Wasserstein GAN

Accuracy with +/- part

CNNs are good: fast and high quality

We can learn language-independent features, we can train at one language and use the model for another

https://github.com/ccsasuke/adan

## QA III (section)

### Joint Multitask Learning for Community Question Answering Using Task-Specific Embeddings

http://aclweb.org/anthology/D18-1452

Three tasks: determine answer goodness, find answers similarity, answer selection

SemEval

Using task-dependand embeddings

Shared NN part for different tasks

### What Makes Reading Comprehension Questions Easier?

http://aclweb.org/anthology/D18-1453

There are many QA datasets (more than 30)

### Commonsense for Generative Multi-Hop Question Answering Tasks.

http://aclweb.org/anthology/D18-1454

NarrativeQA

44% answers are spans in the text, 42% require outside knowledge

Elmo and self-attention are important

ConceptNet: KG with 28M edges and 37 relation types

### Open Domain Question Answering Using Early Fusion of Knowledge Bases and Text.

http://aclweb.org/anthology/D18-1455

Answer factual questions posed in NL

open domain

search in web-scale data

it's different from text comprehension

Wikipedia is a data source

...

Retrieve relevant information

Freebase knowledge base - structured data source

### A Nil-Aware Answer Extraction Framework for Question Answering

http://aclweb.org/anthology/D18-1456


