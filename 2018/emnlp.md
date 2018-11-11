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

Deliberate choice to mislead

...

Colombia cross cultural deceptioc corpus

64% F1 gives acoustic and embeddings, we can get 74 with using personal features

Machnies perform better than humans

Humans are better in the case of sensitive questions

## Semantics I (section)

### Reasoning about Actions and State Changes by Injecting Commonsense Knowledge

http://aclweb.org/anthology/D18-1006

World state changing during the process, mental picture of the process, not explicit information

Datasets are restricted, propara dataset, processes descriptions, annotations with states and entities

The dataset contains NL, many topics, reach vocabulary

How to build a model? 

We want to predict states of entities, predict changes of states, predict state change by paragraph

Encoder gives actions encoding, decoder gives small vocabulary of states

bi-LSTM, bilinear attantion for encoding

Decoder greedy strategy works ok, but it can be inconsistent

We need to inject common sense to network

Global common sense: you can't recreate or do smth after destroy

Topic specific logic: uses semantic verb labeling (VerbNet), gives Bayesian network

Prune bad branches, re-weight branches, beam search, many steps prediction

Rule-based gives 35.9 F1. 50 F1 can be achieved without common sense, common sense gives +5

Errors: implicit reference, coreference, knowledge retrieval

https://github.com/allenai/propara

### Collecting Diverse Natural Language Inference Problems for Sentence Representation Evaluation

http://aclweb.org/anthology/D18-1007

NL inference, premise + hypothesis => entaild or not

Dataset snli and multi nli; large scale datasets

dnc collection, decomp.io

Dataset based on VerbNet (manual curation)

bi-LSTM and max pooling for extract sentences

### Textual Analogy Parsing: What's Shared and What's Compared among Analogous Facts

http://aclweb.org/anthology/D18-1008

Automatic visualization

Similarity in shallow semantic structure

Analogy frame, shared content, compared content

Public dataset from manually annotated wallstreet journal dataset

Graph based model, extract quantity entities, guess about agents, try to merge/build connections

graph is analogous with analogy frame

...

evaluation by triples

F1 ~62

### SWAG: A Large-Scale Adversarial Dataset for Grounded Commonsense Inference

http://aclweb.org/anthology/D18-1009

SWAG dataset

adversarial filtering

get data from video caption

how to get wrong answers? adversarial filtering

get similar style answers, but different semantics

Manchine/human text classifier, replcar machine written, iterate until converting

bi-LSTM with POS instead of rare words

ELMo embeddings and esim give 60 accuracy, humans get 88

OpenAI performs much better

### TwoWingOS: A Two-Wing Optimization Strategy for Evidential Claim Verification

http://aclweb.org/anthology/D18-1010

## Language models (section)

### Deterministic Non-Autoregressive Neural Sequence Modeling by Iterative Refinement

http://aclweb.org/anthology/D18-1149

Autoregressive model

LSTM with attention is a strong baseline

RNN based problems - hard to aprallelize

there are many great models with CNN and attention without recursion

Non autoregressive models: model probabilities are independent from the previous words

...

Use supervised methods which optimize cross-entropy

...

### Large Margin Neural Language Model

http://aclweb.org/anthology/D18-1150

Word embeddings, LSTM, softmax with cross-entropy

Large margin models

### Targeted Syntactic Evaluation of Language Models

http://aclweb.org/anthology/D18-1151

RNN doesn't know about syntax/structural represenation

Exisiting metrics (perplexity) isn't enough

Many attractors makes performance worse???

...

### Rational Recurrences

http://aclweb.org/anthology/D18-1152

Weighted state automata is well study and iterpretable, no threory by RNN

Strongly typed RNN

Hidden states as string scores

RNN is rationale if recurent update can be charaterized by set of automata

...

### Efficient Contextualized Representation: Language Model Pruning for Sequence Labeling

http://aclweb.org/anthology/D18-1153

ELMo, improved everything without annotations

...

Layer-wise dropout

...

## IR / text mining (section)

### Improved Semantic-Aware Network Embedding with Fine-Grained Word Alignment

http://aclweb.org/anthology/D18-1209

Networks are everywhere, social networks, nodes are users

Embeddings for the nodes

Textual information which is associated with nodes can be helpful

Previous works ignored textual information, they used sentence-level embeddings

Two types of embeddings: structural and textual

Text embeddings is a linear combination of the word embeddings

Affinity matrix, scores are multiplication of smth (embeddings)

node2vec model

Structural embeddings were used as a parameter for training text embeddings

### Learning Context-Sensitive Convolutional Filters for Text Processing

http://aclweb.org/anthology/D18-1210

CNN is a promising block in both encoders and decorders

CNN can extract n-gram features, they are flexible to context size, and they are fast (you can use them in parallel)

CNN limitation: weights are independent on text

Add context aware filters

Adaptive CNN (ACNN)

QA context, build Q and A embeddings by those CNNs and than matching and output

It's related to attention mechanism

Experiment: document classifiction, sentence matching

Works well on document classification, compared only with CNN-based approaches

WikiQA

It works much better with smaller amount of filters and works much better when we have not so many filers.

Key result: filter generation mechanism, which improves traditional CNN

### Deep Relevance Ranking Using Enhanced Document-Query Interactions

http://aclweb.org/anthology/D18-1211

Use only text, no clicks/links. Sometimes such resources aren't available

Deep relevance matching model

Document terms compared to query terms (~similarity matrix). Term score layer, input size = query term size, we inject document data there

Relevance score layer (final)

Use cosine similarity, it's hard to normalize, hard to do end-to-end training.

Attention-based elemnt wise, softmax by documents terms, attention based doc encoding, it's deferrentiable

using pooling???

Using additional features, like BM25, negative sampling etc

Datasets: BioASQ, TREC robust

Gives: +5 nGCD to just td/idf, +1..2 to compare with usuaul deep learing systems

it's statistically significant

Sometimes deep learning is worse than just usual inverse index

TREC dataset isn't optimal: small and keyword queries (~3 words in an avarage query)

This helps for NL queries

https://github.com/nlpaueb/deep-relevance-ranking

### Learning Neural Representation for CLIR with Adversarial Framework

http://aclweb.org/anthology/D18-1212

### AD3: Attentive Deep Document Dater

http://aclweb.org/anthology/D18-1213

Predict document publishing time

Sentence, context embeddings (bi-LSTM), syntactic embeddings, ... , (s-GCN), (at-GCN) ...

Ordered event model

...

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


