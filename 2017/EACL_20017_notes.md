# Заметки с EACL 2017

##### Содержание
[Word embeddings](#word_embeddings)  
[Summarization](#summarization)  
[Multiwords expressions](#miltiword)  
[Universal dependencies](#ud)  
[Probability topic models and user behavior](#topicmodel)  
[Coreference](#coreference)  
[Information retrieval and information extraction](#ir)  
[Parsing](#parsing)  
[Summarization-2](#summarization2)  
[Words, peactures, common sence](#wordpic)  
[Knowledge bases](#kb)  
[Word representation](#wordrepr)  
[Embeddings](#emb)  

Bonus track: 
[Schütze: Don't cram two completely different meanings into a single !&??@#^$% vector! Or should you?](https://twitter.com/rctatman/status/850250053063135234)

<a name="word_embeddings"/>

# Word embeddings (word vector space)

[Слайды](http://people.ds.cam.ac.uk/iv250/tutorial/wv-tutorial.pdf).

## Введение
Иногда word vector space сложно использовать в приложениях - антонимы находятся рядом. Например, мужчина-женщина, запад-восток и так далее.

http://babelnet.org/ - мулиязычный ресурс со словарями, семантикой и базой знаний, synset'ы.

http://paraphrase.org/ - ресурс с большим набором перефразировок.

Unsupervised подходы дешевле - не нужен размеченный корпус.

Нужно объединение двух подходов: unsupervised + размеченные ресурсы.

## Обучение по контексту
Хотим извлекать признаки, которые будут примеными ко многим задачам и инварианты к языку.

Соотвествие слово->вектор в многомерном пространстве.

Слова имеет близкие значения, если они встречаются в одинаковом контексте.

Mikolov статья 2013 года.

Можно использовать негативные примеры в обучении. (случайное слово в контесте из корпуса).

Типы контекстов: bag of words (BOW); с позициями относительно текущего слова; с синтаксическими зависимостями; с синтаксическими зависимостями, но связи с предлогами удаляются.

Cross language dependency based spaces (EACL 2017 статья).

Больше веса для глаголов и пралагательных в контексте, это помогает для улучшения качества. Статья Schwartz NAACL 20016.

Для разных задач помогают разные типы контекстов. Также можно играть с размерностью пространства.

Melamud CONLL 2016, использовал bidirectional LTSM.

Симметричные pattern'ы, статья Schwartz CONLL 2015.

Context2vec.

## Лингвистические ограничения
Все зависит от корпуса.

Используем структурированые знания (источники?).

Wordnet - это набор synset'ов, каждый из которых соответствует некоторому концепту. Слово может участвовать в нескольких synset'ах. Внутри wordnet'а есть отношения: гипероним, гипоним, принадлежность к domain'у, мероним (часть-целое) и так далее. Гиперонимы образуют иерархию. Прилагательные сложно ложаться на иерархию.

Проблемы источников типа wordnet: дорого обновлять, ограниченный словарь, плохо описывают конкретные предметные области и последние изменения в языке.

Wikipedia полезный источник данных. Есть ссылки, многоязычность много сырой и структурированной информации.

Wictionary намного больше, чем wordnet, хорошое покрытие языков, очень избыточные.

omegawiki близко к wordnet'у, плохое покрытие.

Bablenet - это слияние всех источников, похоже на wordnet, есть API. Есть live-версия (последняя, видимо, не очень стабильная).

Paraphrase база с шаблонами на 16 языках, извлекалась из параллельных корпусов. Несколько типов: лексический, перефразировка, синтаксический с нетерминалами. В базе есть scores.

Google ngram база. Ранжированные перефразировки.

Wordnet имеет хорошее качество.

## Комбинирование подходов
Обобщать по конкретному словарю сложно.

Можно соединить два подхода. Основные способы: "тяжелый" (все делаем совместно), пост-обработка (после построения векторов двигаем их).

Оба подхода используют одинаковые входные данные.

Yu and Dredze ACL 2014.

Интерполяции по источникам знаний.

Парное сходство по примерам. Fool/stupid ближе, чем fool/smart.

Нужно отличать similarity, relatedness и association. Для классификации и topic modeling можно не отличать.

Пост-обработка. Двигаем слова после построения векторов и оптимизируем фунцию для пар синонимов. При этом не должны сильно поменять построенные вектора.

Mrksic NAACL 2016. Функция оценки, которая базируется на синонимах, антонимах и исходных векторах.

Wordnet хорошо для одноязычного случая, babelnet для многоязычного.

Paragram подход (Wieting 2016) добавляем "негативные" пары синонимов (вроде бы, случайные).

Ограничения для конкретной модели помогают с омонимией.

## Последняя часть
Если использовать только ограничения и случайные вектора, то это может неплохо работать (очень зависят от языка).

Многоязычные вектора работают неплохо даже при условии недостатка ресурсов.

SimLex данные (есть для русского). Не для всех языков хватает данных.

Диалог + отслеживание его состояния (slots, тип вопроса). Рассматриваем диалог как распределение таких состояний. Делать по точным совпадаением помогает очень плохо. Семантичесие словари помогают для маленьких данных. Можно обучить нейросеть.

offtop: можно перейти от классификации на много классов к большому количеству бинарных классификаций. Relu фунция активации max(0,x). CNN помогает обучать представления. Сегменты слов в NN. 

Wizard of Oz dialog dataset.

Glove vectors.

Морфология с небольшой коллекцией размеченных данные работает хорошо. Оченб помогает для немецкого.

Vendrov ICLR 2016 (частичный порядок в векторном пространстве).

## Омонимия
Есть проблема с омонимией.

Разделять значения для слов. 

Можно делать unsupervised кластеризуя слова по контекстам. Нужно зарнее выбрать число кластеров (число значений) для каждого слова.

Если использовать базу знаний, то заранее точно знаем сколько значений у конкретного слова и детали про них.

Pagerank для wordnet o_O.

Часто замеряют на искусственных данных и результаты нерепрезентативны.

Можно это обучать для многословных фраз и для конкретной предметной области.

Тут еще много чего было интересного, но я потерял нить.

<a name="summarization"/>

# Summarization

## Часть 1
wiki статьи, берем статьи их summary. Пытаемся сгенировать похожее.

Берем части подсекций статьи, Биграмы секции, потом документа потом юниграмы. 

Метрики качества предложения и similarity. Много признаков предложения: topic hierarchical model, позиция в тексте и так далее.

LexRank алгоритм.

Замена embeding'ов на кластеры слов.

Rouge 1,2,3,4 оценки.

Memog giannakopoulos 2008

Китайский язык разбиваем ровно по одному символу. Среднее слово в китайском два символа.

Оценка человека для пары summary. Что выглядит лучше.

Multiling15

Weaved baseline (WTF?)

## Часть 2
Используем embeding'и в topic modeling

Content linking: vectors, traditional (???)

LDA

Кластера для предлежений (парное сравнение предложений).

Сумма слов = весу предложения.

## Часть 3
Summarization для отзывов, twitter'а и так далее

Ультра-сжатие (не более 140 символов).

Данные - это контент пользователей. Много жанров.

Удаляем emojis и картинки. Рассматриваем только текст.

Три класса + = -

Ранжирование предложений, sentiment шкала, ранжирование по sentiment'у.

Ручная разметка. Три критерия: содежание, читабельность, responsiveness.

Проблемы: в твиттере много шума, ирония, сарказм.

Корпус 400 документов без cross-checking.

Часть 4: ML подход для оценки summary.

<a name="miltiword"/>

# Multiwords expressions

## Multiword классификация (многоязычная)
Есть compound'ы и есть multiword'ы (нужно различать).

13 классов: организация, локация и так далее.

Рассматриваем классификацию в контексте мониторнига новостей. Выражения рассматриваем вне контекста.

43 языка.

europe media monitor (EMM), name entity hierarchy (события, локации, продукты и так далее).

Брали данные из bablenet, полуавтоматический процесс, маленькая ручная разметка, 200 для родного языка, 200 для инглиша. 5 аннотаторов.

kappa 0.85 (согласованность аннотаторов).

baseline: косинус + простой поиск (?)

Использовали SVM для многих классов

Рассматривали признаки для конкретного языка и языконезависимые признаки.

Рассматривали topic, класс слова, категория(?). Bag of words, tfidf.

Делали бинарную классификацию для каждой пары (зачем?).

10-fold shuffle spli cross falidation

75/25 test/train

SVM + tfidf работают хорошо.

Языко-независимые признаки помогают, для "маленьких" языков языко-зависимые признаки не работают. 

## Двуязычные emebedding'и для извлечения коллокаций
Коллокация - это пара лексических единиц. Один базовый/свободный, а второй зависит от базового.

Для их извлечения нужно обучение. Strong tea/powerful car.

Сложно комбинировать для разных языков, в разных языках используются разные колокации.

Хотим обучить мультиязычные embeddings на параллельных корпусах.

Моноязычные кандидаты, токены->леммы.

word2vec многоязычный.

Используем двуязычные словари, которые содержат данные с вероятностями перевода.

Использовали: лемматизация, POS-tagging, Universal Dependepcies. Рассматриваем паттерны: NOUN+ADJ, VERB+OBJ, NOUN+NOUN.

t-score (?), использовали логарифм правдоподобия.

Выравнила по паттернам (тут потери, так как части речи меняются в зависимости от языка), выбирали N лучших.

Корпус: opensubtitles (OPUS), 13 миллионов предложений.

MaltParser+UD

Linguakit (инструмент для испанского).

Baseline по словарям (?). Видимо, используем переводы конкретных словосочетаний из словаря.

Два ревьюера, для baseline'а согласие 90+, для основного подхода 80.

baseline - хорошая точность, плохое покрытие.

Источники ошибок: preprocess, gender, опечатки, качество модели, антонимы, чай/кофе, mixed varieties (?).

73 F-мера, 88.9 точность.

## Исследование многоязычных лексических ресурсов для задачи про композиционность multiwords
Композицонность. Можем ли получить значение фразы из ее слов. Может не зависить от слов вообще, может от части, можем от всех.

Мультиязычные ресурсы. Token level ресурсы нужны.

Совпадение строк, требует только словари, не требует ничего от языка, не нужны корпуса.

Изпользуем переводы слов, неточное сопадение по морфологии.

Можно мерить схожесть строк разными способами: LCS, lev1, lev2, SW. LCS работает лучше всего.

Итого пытаемся переводить все словосочетание или по слову и смотрим насколько результаты похожи.

Panlex ресурс для переводов, 54 языка.

В работе рассматривали 10 языков, + 10-fold cross-validation.

Результаты хорошие но не идеальные. Результаты сильно зависят от языка.

Используем дистрибутивную семантику aka embeddings. Сравниваем вектор словосочетания со средним вектором по словам.

Комопозиоцнность можно мерить непрерываной величиной.

ENC данные, EVPC данные, GNC данные

Подход через схожесть строк очень помогает в композиции.

Далее были истории про разные значение разных слов и разные способы это выразить/обобщить. Например, слово up.

Итого: комбинация работает лучше всего, из переводной неоднозначности нужно брать лучший вариант, 10 языков потому что 10.

В конце было про PARSEME shared task. Много языков, какая-то лицензия. Хорошо работал transition-based подход.

<a name="ud"/>

# Universal dependencies

## Инфраструктура

universaldependencies.org

70 корпусов,50 языков (есть русские корпуса с эллипсисом).

разные лицензии у разных корпусов

POS + dependecy отношения храним в корпусе 

Много разных типов тектов: новости, wiki, fiction/non fiction, блоги, библия, legal.

Наследовали формат CONLL

Есть metadata уровня предложения.

Явно представлен текст предложения.

В данных присуствуют недревесные зависимости.

Есть дополнительные нулевые вершины (эллиптические).

Все открыто (обсуждения и так далее), все лежит в гите, один корпус-один репозиторий гита.

Есть официальный цикл релизов, много тестов для валидации данных.

Поддерживается целая экосистема для данных: визуализация, аннотации, поиск и так далее.

Syntax net привязан к этим данным.

Медианная точность по именованым связям 81%, в среднем 79%. Японский язык работает хорошо.

Есть web доступ, API доступ и так данее.

PML query tool, например для поиска непроективных конструкций.

udapy для визуализации.

## Использование
Помогает обучать и оценивать парсеры.

Udpipe, syntaxnet - out of box парсеры. Они используют моноязычный подход (?).

Есть многоязычный подход, universal parsing, тренируем на одном языке, тестируем на другом.

Для многоязычного подхода нужны согласованные аннотации. Не всегда нужно хорошее POS-tagging.

тысячи языков без корпусов (?)

wang eisner 2016, the galactic dependencies

Синтез новых языков

Reddy 2016, от синтаксиса к семантике, QA, семантические представления

Vulic 2017, синтаксис для embedding'ов, 

bible корпус содержит 1000 языков

Не требуется много данных для приемлего парсинга.

<a name="topicmodel"/>

# Probability topic models and user behavior

david m. blei

Полезно для организации, визуализации, summarization, поиска, понимания, предсказания (topic models).

Визуализация важна, понимание тематической структуры, аннотация/

Визуализирование коллеции по группе слов.

Topics by time(?), unsupervised подход, сбор событий из мира, аннотирование изображение, анализ генома (???)

Люди читают документы, это можно предсказывать и рекоммендовать.

Документ может соответствовать нескольким темам.

Latent dirichlet allocation (LDA)

Topic - это распределение по словарю.

Для документа можно ввести распределение по topic'ам.

Мы не можем наблюдать всю это.

LDA - это graphical model, поиск факторизации для совместной вероятности.

Для одного слова можно понять его распределение по topic'ам, для документа тоже и для корпуса тоже.

Рассматриваем апостериорную вероятность.

Есть много методов для апроксимации и LDA

Фиксированное число topic'ов.

Если замерять самое частотное слово для конкретного topic'а, то это может быть очень показательным.

Мы хотим получить low dimensional представление документа.

Цель LDA: отнести документ к небольшому количеству topic'ов, и найти небольшое количество слов, которые относятся к topic'у с большой вероятностью. Цели противоречат друг другу.

Есть другие подходы: latent semantic analysis, mixed membership model, PCA. Некоторые независимо придумали генетики o_O

LDA - важная часть многих приложений.

Последние алгоритмы для graphical models расширяются на big data

collaborative topic models, используют LDA

Общие данные, данные о поведении юзеров, статьи которые читал юзер могут помочь людям лучше понять topic'и документа. Помогут находить новые документы, описывать юзеров, находить важные документы.

Подстраиваемся к поведению юзеров, рекоммендуем статьи новым людям несмотря на исходные предположения.

Без текстов нет базовых рекоммдаций, без данных от юзеров мы не можем находить новое.

mendeley.com - ресурс с открытыми текстами.

251k документов, 500 topic'ов, 80k юзеров.

Оценивали работу вручную + спрашивали юзеров.

Arxiv.org данные с кликами. Разные типы кликов.

<a name="coreference"/>

# Coreference

## Interlay of coreference and discourse

Prague книга про coreference.

Много корпусов: MUC, ACE, Ancora, onto notes(?). 

Много типов корпусов

## Три вопроса к анафоре и кореференции
Руслан Митков

Насколько полезно для NLP, как оценивать, какие связи сложно находить

Анафора и кореференция - это разные понятия.

Пытались интергрировать разрешение местоимений в NLP приложения. И оцеивали насколько это помогает.

MARS algorithm

1200 местоимений из 48000 слов.

Для summarization есть небольшоу улучшение.

t тест, статистическая значимость (t test, statistically significant).

Для term extraction получаем +5% f-меры, для классификации +5-10%, но улучшения статистически незначимы.

Гипотетическои можно рассмотреть идеальное разрешение анафоры, это очень помогает для tfidf (статистически значимо +20%, но непонятно для чего именно :) )

Bart algorithm. Если разрешать кореференцию с его помощью то он даже немного ухудшает в одном из приложений.

Иногда улучшает но статистически незначимо.

!Про то как оценивать.

Сложно воспроизводить многие результаты, очень разнятся цифры, согласованность очень низкая

Важно понимать насколько данные сложны и оценивать это.

Смотреть на данные до исследований, делать исследования прозрачными и объективными.

Байка про журнал с негативнми результатами. 

## Кореференция для помощи машинному переводу

Gender-related проблемы в переводе.

Контекст важен.

Phrase-based подход.

Neural translation machine.

Для оценки сравнивают машинный и человеческий переводы.

BLEU metric (n gram precision)

Ограничения от кореференции.

Corefence similarity score.

Find alignment of mentions.

Качество перевода улучшается с качеством разрешение кореференции.

Переранжирование гипотез, рассматриваем документ целиком.

Удаляем предложения с одинаковыми упоминаниями (mentions), beam search, добавляем предложение за предложением

Пост-обработка, более точная, работа с кластерами.

Разброс в экспериментальных данных, автоматические метрики + человеческая оценка

Acuracy of resolution is quite small (?)

<a name="ir"/>

# Information retrieval and information extraction

## Китайские тесты и автоматические ответы на их вопросы

gaokao - это китайский аналог ЕГЭ.

9 предметов, background вопроса, сам вопрос, варианты ответа

Сложные вопросы, сложно понять background, все сильно зависит от внешних знаний, много кандидатов для ответов

Обучение 50000+ high quality(?) вопросов, тест 744 вопроса (entity вопросы/sentence вопросы)

Два подхода: information retrival, нейронные сети

IR pipeline: классификация запроса, оценка релевантности для каждого кандидата, выбор лучшего кандидта

IR ресурсы: baike, book, tiku

нейросеть permanent provisional memory networks

similarity judger, sentence encoder

Эксперименты: нейросети хороши, но в комбинации с IR еще лучше (для entity запросов).

Тестировали много подходов: RNN, LSTM, GRU...

Комбинированный подход работает лучше и стабильнее

Качество работы около 45% (accuracy), люди могут 60%, то есть работает оно хуже чем люди

## Non factored answer reranking
У большинства читателей есть non-factored вопросы.

Недостаток данных.

Нужно перкставить ответы юзеров, это почти ранжирование, но нас интересует только один первый ответ.

Featured based подходы, нейронные сети

Doc2vec + MLP(?), LTSM

Можем ли мы их комбинировать?

10k yahoo вопросов, 13k вопросов из ubuntu, есть сложные вопросы

baseline random, поиск кандидатов по tfidf + косинусная метрика

Векторы для параграфов

MRR метрика

Bidirectional gated RNN, QA, cross entropy loss

Получилось заметно лучше чем baseline

GRU сложное, но работает плохо

Pairwise similarity, это помогает.

Discourse features, discourse marker model jansen ACL 2014

Sentence + cross-sentence уровни, skipgram

Discourse признаки работают довольно хорошо, немного лучше baseline

Ошибки часто основаны на авторпе вопроса, еще мы не учитываем screeshots, картинки, code snippets

Основано на категориях (?), partial match вопроса и ответа (?)

## Chains of reasoning over entities, relation ans using RNN
Корпус, entity identify, отношения

Универсальная схема

Факты извлеченные из путей в KG.

Path ranking algorithm

RNN

Ограничения, scalability

...

max pool, avg pool, logsumexp; avg работает плохо

## Распознавание методов рекламы лекарств
Поиск рекламы лекарств в social media

Unwanted reaction clearly associated

Это позволяет изучать side effects действия лекарств

Мониторинг реакции over time

Быстрые ответ на реакцию

Train 5723, test 1874 (предложений)

Данные маленькие

Контекст очень важен, terrible headache, headache go away

Разговорный жанр текстов, неграмматичные тексты, 

Для каждого слова begin/middle/end объекта

Bidirectional RNN

word term distribution

Добавляем дополнительные данные

Embeddings для слов

dbpedia

ADR oracle, независит от контекста

Precision 55% без контекста

LTSM, embeddings, word2vec, blekko

blekko работает лучше всего, медицинский корпус

Корпус очень важен для построения embedding'ов

dbpedia embeddings помогает

Небольшие данные работают хорошо

Час разметки, F-мера 74.2

Даже небольшая разметка очень помогает, active learning (?) помогает

## Понимание mental health condition в условии ограниченных данных
Задача классификация важна

Нужно много данных

Предсказание mental conditions (суицид и так далее).

логистическая регрессия, нейросети, много ответов (не softmax, так ответы независимы), N-грамы

ROC-кривая для оценки

MTL помогает

<a name="parsing"/>

# Parsing

## Многоязычный parsing
Для разных языков разное количество данных.

Annotation projection из одного языка в другой

Тренируемся на одном языке и используем параллельные корпуса, это работает плохо(?)

Graph vs tree parsing (?)

Матрица оценок для связей.

tensor transformations (?)

Оценки для одноо языка + cross lingual оценка

graph based подход

## Parsing UD без обучения
Много связей очевидны

UD есть особенности

Unsupervised/rule based подоходы для простого baseline

Pagerank для слов

Два шага: decoding слов по ranking, ? (??)

Оценка направлений для связей, разделяем content words/function words, используем small teleport prob in PageRank(??)

Мы оцениваем во время runtime и строим частоты слов на ходу

Лучше чем baseline, работает хуже чем supervised но не сильно

5% хуже чем supervised, в одном языке даже лучше

## Delexicalized parsing
Обучаемся на языках с большим количеством данных, парсим языки где данных мало

Graph based подход, строим spanning tree

Строим представления слов, 

Модели специфичны для языка

Представления для слов не зависят от языка

character based подход

Используем только morpho/syntactic признаки

co-occurencies matrix

sequential context/syntactic context, можно их смешать

eisner алгоритм для поиска MST

Улучшение довольно незначительное (?)

<a name="summarization2"/>

# Summarization-2

## Lexical summarization by neural ranking
Замена сложных слов более простыми

Поиск сложных слов

Генерируем кандидатов на замену

Выбираем лучших по контексту

Ранжируем по простоте ответа

Параллельные корпуса + embeddings

11000 docs, 7 миллионов (?) слов

использовались wordnet синонимы

Unsupervised nboundary ranking?

Бинарная классификация, boundary distance (??)

Neural net ranking, два кандидата - это input

SubIMDB (subtitles ranking) n grams 

lexmark

simplicity compare

3 слоя,8 узлов в каждом

в целом результаты хорошие, но есть плохие части (?)

точность хорошая

Lexenstein

## Limits of automatic summarization according to rouge
state of the art подходы unsupervised

Жадные алгоритмы набора summary

perfect score очень сложно получить теоритически

Люди плохи в summarization

оптимизация ROUGE метрики NP-сложная (сводиться к weighted dominating set)

## crowd source iterative annotation
Абстрактно делать summarization сложно

Создание корпуса, pipeline, input narratives (?)

абстрактные summaries, extractive summaries

Выравнивание фраз

Согласие между аннотаторами 

90% согласие, но иногда одно и тоже выражают разными способами

итого: dataset, 1088 summary pairs abstract, 6173 выравненных фраз

## broad context language model
Предсказание слов требует контекста (broad discourse context)

Задача понимания (copmrehension task)

Attetion sum reader kadlec 2016

Lambada dataset, baseline самое частое слово в контексте 11.7 (непонятно что за метрика)

44.5,49, 51.6 системы

86 люди

Детали: кто говорит, кореференция, внешние знания

## Negation detection
Токен - это часть scope'а (?)

bidirectional LTSM подход

корпуса медицинских текстов, два английских, один китайский

transition-based подход

token-level f-мера

scope-level оценка

Во многих предложениях все определяется пунктуацией

Rule based система - baseline

Легко по пунктуации, сложно без нее

Хорошо работает в легких случаях (сюрприз!)

проблема: очень разнные подходы к разметке

## Cross lingual open infromation extraction
Перевод

Нам важен факт на другом языке

cross lingual open information extration

Перевод, parsing, extrction (?)

end to end подход (?)

encoder/decoder подход (?)

syntaxnet + predpatt (IE тулза)

sequence to sequnce model

Predictive pattern aproach, смотрим на синтаксическое дерево и извлекаем по нему факты

Linearized predpatt

Moses (статистический машинный перевод), syntaxnet, predpatt

BLEU (для оценки перевода) + F1-score

19, 21.5 $

F1 по токенам: 28..33.6 %

<a name="wordpic"/>

# Words, peactures, common sence
Много визуальных данных, слова используются для коммуникации (?)

Measure understanding 

Диалог с визуальными данными

Обучить машину понимать общий смысл проиходящего

Ответы находятся в картинках, без картинок ответ не находится

CNN для картинок, RNN LTSM для текстов

Baseline 4.74 лет, в среднем вопросы для 9-летних

На абстрактные вопросы отвечать сложно

Там было еще что-то про абстрактные картинки, их генерацию, что одно и тоже можно разными картинками выразить

<a name="kb"/>

# Knowledge bases

## Multi level representation for fine grained typing of kb entities

У нас есть entity с id, поиск metions, получаем тип entity, author, politic (??)

Entity representation, скрытый слой, результат

Multilabel, сигмоида а не softmax

корпус, wang2vec

упоминание fasttext

улучшение на уровне entity

word level reprsentation, word level word2vec

subword level fasttext

Используем charater leverl representation для CNN

Dataset содержит 200 000 entities, freebase dataset

Синтаксис важен

CNN работает лучше для неизвестных слов, multilevel помогает

context тоже помогает (?)

## Contrastmedium algorithm taxonomy inducyion from kg with just a few links
Удаляем слова перемещением контраста (??)

+3-5% улучшение для точности

## Probabilistic inference for cold start with prior knowledge
Строим KB из корпуса, важно для QA, поиска и тэдэ

Cold start - это данные плюс схема, 

shared task, TAC 2015 cold start KB population track overview

Hop 0 query, ищем супргов/детей

Hop 1 query, куда дети ходят в школу

Большой pipeline неточных компонент

Есть ошибки общего характера, много ДРов, 8 браков и так далее

Сложно исправлять ошибки, очень разные источники ошибок, но нужно их исправлять

Знания из внешнего мира помогают, используем entity popularity, варианты имен, упоминания имен(?)

Relation cardinality

EDL features(IE framework), entity linking confidence, расстояние редактирования, membership clustering (?).

Re source algorithm, типы отношений, confidence, argument mentio level(??)

F-мера плохая, hop-0 38.4, hop-1 24

## Generalization to unseen entities and entity pairs
Текст - это входные данные, нужно извлечь entities + relations

Text mentions coreference+relation pipeline

Обучаем embeddings для всего

Случайная генереция "негативные" примеры

Pattern encoder

Query independent признаки, mean pool, max pool

Query dependent

<a name="wordrepr"/>

# Word representation

## String baseline for multilingual embedding for sentence alignments
dice metric

моноязычный контекст и многоязычный контекст

Bible corpora

Выравнивание слов, использование словарей

Используем sentence ID, verse ID 

SVD, SGNS

## Online learning of task specific word representation with a joint biconvex passive
passive aggressive algorithm

Заранее обученные embedding'и не всегда работают хорошо

Каким образом обучать для конкретной задачи

Build from scratch with big data

Обучаем существующие embedding для контекста конкретной задачи

soft margin

re embedding passive aggressive

Learning rate считаем по Лагранжиану o_o

Embeddings matrix

Alternating convex search

syntactic data experiments

Улучшение для классификации

## Nonsymbolic text representation
Базовые части слов, символьные n-грамы, рассматриваем несколько токенов, все символьные n-грамы

wiki использовалась как корпус

cross-token символьные n-грамы

end to end подход

Representation learning

Multiple random segmentation (?)

Небольшое улучшение f-меры

можно обучать хорошие embedding'и без токенизации

Но с токенизацией все равно работает лучше

<a name="emb"/>

# Embeddings

## Embeddings for rare and unseen words by lexical resources
Выражаем семантику в векторном пространстве

Domain specific слова, слова со сложной морфологией, морфологическая трансформация слов

Есть много внешних ресурсов, babelnet 

Извлекаем знания из внешних ресурсов и используем их

Lexical source as a semantic network (?), строим semantic landmarks, строим вектора

Для semantic landmarks используем персонализированный pagerank (??)

Формула: используем начальное приближение (если есть), используем линейную комбинацию семантически близких слов, близкие слова ранжированы по расстоянию

## Large scale evaluation of dependency based
Dependency filtering vs dependency typed

???

## Hyperonyms + embeddings
Классификатор для гиперонимии по embedding'ам

state of the art F1 0.85 но на опредленных данных, на других данных все заметно хуже

Анализ этих данных

Нормализация другим dataset'ов

Модели: logistic regression + SVM

baroni хороший dataset

## cross lingual embeddings from syntactic data
UD дают языко-независимые синтаксические данные

word vectors для разных языков в одном пространстве

simlex dataset

А вообще тут общая идея в том, что синтаксис помогает для embedding'ов

## cross language plagiarism detection
Поиск похожих цепочек слов

jaccard distance (?)

## semantic morpho in embeddings
morpho similarity

Есть морфологически сложные языки

skipgram miklov подход

bojanowski fasttext 2016

prop2vec

Lemma vectors encode semantics