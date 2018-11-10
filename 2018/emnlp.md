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

### A Unified Syntax-aware Framework for Semantic Role Labeling

http://aclweb.org/anthology/D18-1262

Syntactic structure vs semantic structure

Argument identificaition, ..., classification of syntactic links???

Syntax agnostic approaches vs syntax aware approaches

...

### Semantics as a Foreign Language

http://aclweb.org/anthology/D18-1263

Semantic dependency parsing

There are three representations

Extract semantic argument predicate relations

Graph structure, words are nodes, edges are relations. It's not a tree, it can be not connected

Consider it as a machine translation task

Model: seq2seq, linearization

Raw sentence into linearization, three models, we can share data. We can translate between different representations

seq2seq bi-LSTM with attention

linearization by using braces, depth first representaion

Models for non-tree/non-reachable parts??

Artifical shift edge, it doesn't exist in reality, but used for formalism

re-entranceof words, we need unique representation, use relative to previous word index and surface form

Multi-task learing is a useful trick here

Can convert between different representaion quite well: 90+ F1

PSD contains less data

### An AMR Aligner Tuned by Transition-based Parser

http://aclweb.org/anthology/D18-1264

JAMR aligner, rule based

...

Proposed smth better, which is embeddings based

Transition based parser

### Dependency-based Hybrid Trees for Semantic Parsing

http://aclweb.org/anthology/D18-1265

Transform to machine interpretable representation

FunQL, functional query language

...

### Policy Shaping and Generalized Update Equations for Semantic Parsing from Denotations

http://aclweb.org/anthology/D18-1266

## NER (section)

### Marginal Likelihood Training of BiLSTM-CRF for Biomedical Named Entity Recognition from Disjoint Label Sets

http://aclweb.org/anthology/D18-1306

Biomedical papers contain a lot of relevant information

NER is a first step to extract info

5 entity types

Embeddings layer, Bi-LSTM, CRF

Concatenation of two datasets

Multi-CRF output, two CRFs for each dataset

Share information between datasets

Predicitions merge process

Joined model helps

MedMentions dataset, 19 entity types

Train over multiple datasets can be helpful, even when labels are different

Marginal CRF performs better

### Adversarial training for multi-context joint entity and relation extraction

http://aclweb.org/anthology/D18-1307

Identify named entities and relations

Adversarial training helps tp improve robustness by adding peturbations to input, it was helpful in NLP

Character embeddings layer, LSTM, label embeddings

Similarity matrix, tokes x tokens * relations for relations extraction

Add perturbations to the embeddings layer

DREC dataset

Performs close to hand crafted features or even better

Fater training

### Structured Multi-Label Biomedical Text Tagging via Attentive Neural Tree Decoding

http://aclweb.org/anthology/D18-1308

Multiple labels from medical vocabulary, which has tree format - ontology

Encoder/decoder model

Recursive attention application

Dataset from RCT publications

...

F1 < 0.45

### Evaluating the Utility of Hand-crafted Features in Sequence Labelling

http://aclweb.org/anthology/D18-1310

Heavy feature engineering for a long time

From 2010 deep learing models are popular

Injext text and features (linguistic) to encoder, compute main task and input features

Bi-LSTM, CNN, CRF

Hand-crafted features: POS, gazetteers, word shape, dependecies ... (used one-hot encoding)

Student t-test for significance

Feature auto-encoder helps!

Worse than best result, because the best used elmo embeddings instead of GloVe

Features at output help and it's statistically significant

Auto-encoder features trick can be helpful in many contexts

### Deep Exhaustive Model for Nested Named Entity Recognition

http://aclweb.org/anthology/D18-1309

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


