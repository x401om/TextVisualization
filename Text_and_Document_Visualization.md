#Визуализация текстов и документов
В наше время мы имеем огромное количество источников информации: от библиотек до электронной почты, а также различных веб-приложений.
Визуализация – отличный способ проанализировать подобную информацию. При помощи различных подходов мы можем визуализуализировать такие вещи, как блог, вики-страницы, лента в Твиттере, миллиарды слов, набор бумаг или электронную библиотеку. Так как способ визуализации данных зависит от задачи, которую мы решаем, нам необходимо понимать, какая именно информация нам потребуется при работе с текстом, документами или некоторыми интернет-сущностями. Наиболее очивидной задачей, сопряженной с анализом тектов и документов, очивидно, является поиск слова, фразы или темы. В слабо структурированных данных мы моглибы искать связи между словами, фразами, темами или документами. Для структорированных массивов тектов или документов основной задачей часто является поиск паттернов и выбросов.
В этой статье мы обратим внимание на задачи, связанные с текстами и на различные подходы их визуализации с целью проведения определенного визуального анализа.

##1. Введение
Определим [множественный] **корпус**, как некоторый набор (коллекция) документов. Мы взаимодействуем с объектами этого корпуса. Такими объектами могут быть слова, предложения, абзацы, цельные документы. Также мы можем рассматривать иллюстрации и видео. Чаще всего эти объекты рассматриваются поотдельности, в зависимости от типа задачи. Тексты и документы часто минимально структурированны и могут содержать определенные атрибуты, метаданные, особенно если эти тексты относятся к какой-то специфической предметной области. К примеру, документы имеют формат и часто включаютс в себя информацию об этом документе (автор, дата создания, дата изменения, комментарии, размер и др.). Для того, чтобы делать запросы к корпусу используются специальные системы извлечения информации, которые позволяют понять, насколько каждый из документов релевантен запросу. Для этого необходимо производить некоторые предварительные вычисления, а также интерпретировать семантику текстов.

Также мы имеем возможность подсчитывать статистики по документам. Например, число слов в абзацах или распределение слов по частотам, относительно авторов текстов. Есть ли в тексте какие-то абзацы, в которых повторяется одно и то же слово или предложение? Также мы имеем возможность строить связи между абзацами документов внутри корпуса. Например кто-то спросит: "В каких документах говорится о распространении гриппа?". Это не самый простой запрос – это не просто взять и поискать слова "грипп". Почему? Далее можно искать естественные связи или отношения между различными документами. Какие кластеры тут наблюдаются? Являются ли эти кластеры темами? Похожесть может быть определена в терминах цитирования, обзего авторства, тематики и т.д.

##2. Уровни представления текстов
Выделим три уровня представления текстов: лексический, синтаксический и семантический. Каждый из них требует от нас конвертации неструктурированных тектов в некоторую форму структурированных данных.
- **Лексический уровень.** Лексический уровень основан на преобразовании наборов символов (строк) в последовательность атомарных сущностей, называемых **токенами**. Лексический анализаторы преобразуют входную последовательность символов по данным наборам правил в новые последовательности токенов, которые могут быть использованы в дальнейшем анализе. Токены мокут в ключать в себя символы. n-граммы, слова, основы слов, лесемы, фразы или словесные n-грамы, все с присущими им атрибутами. Много правил может быть использовано для извленчения токенов, наиболее распростронееым из них является конечный автомат, определенные некоторым регулярным выражением.- **Синтаксический уровень.** Синтаксический уровень определяет и теггирует (аннотирует) функцию каждого токена. Мы присваиваем различные теги, такие как позиция в предложении или является ли слово существительным, прилагательным, бранным словом, модификатором или союзом. Токен также может иметь атрибуты, которые говорят о том, стоит ли он в единственном числе, а таеже определяют близость токена к другим токенам. Расширенные теги могут определять дату, валюту, место, персоналию, орагизацию и время. (Рис. 3) Процесс извдечения подобных аннотаций называется Распознованием Именнованных Сущностей (named entity recognition – NER). Богатство и разнообразие лингвистических моделей ведет к широкому разнообразию подходов.- **Семантический уровень.** Семантический уровень включает в себя извлечение смысла и связей между знаниями, полученными на этапе определения структуры на синтаксическом уровне. Цель этого уровня – опрпделить аналитическую интерпретацию текста целиком в рамках определенного контекста или даже вне зависимости от контекста.

##3. Модель векторного пространства
Computing term vectors is an essential step for many document and corpus visualization and analysis techniques. In the vector space model [356], a term vector for an object of interest (paragraph, document, or document collection) is a vector in which each dimension represents the weight of a given word in that document. Typically, to clean up noise, stop words (such as “the” or “a”) are removed (filtering), and words that share a word stem are aggregated together (stemming) [192].The pseudocode below counts occurrences of unique tokens, excluding stop words. The input is assumed to be a stream of tokens generated by a lexical analyzer for a single document. The terms variable contains a hashtable that maps unique terms to their counts in the document.

Count-Terms(tokenStream)1 2 3 4 5terms ← ∅   initialize terms to an empty hashtable. for each token t in tokenStreamdoif tisnotastopworddo increment (or initialize to 1) terms[t]return termsWe can apply the pseudocode to the following text.

There is a great deal of controversy about the safety of genetically engineered foods. Advocates of biotechnology often say that the risks are overblown. ‘‘There have been 25,000 trials of genetically modified crops in the world, now, and not a single incident, or anything dangerous in these releases,’’ said a spokesman for Adventa Holdings, a UK biotech firm. During the 2000 presidential campaign, then-candidate George W. Bush said that ‘‘study after study has shown no evidence of danger.’’ And Clinton Administration Agriculture Secretary Dan Glickman said that ‘‘test after rigorous scientific test’’ had proven the safety of genetically engineered products.

The paragraph contains 98 string tokens, 74 terms, and 48 terms when stop words are removed. Here is a sample of the term vector that would be generated by the pseudocode:
TABLE
###3.1. Computing Weights
This vector space model requires a weighting scheme for assigning weights to terms in a document. There exist many such methods, the most well known of which is the term frequency inverse document frequency (tf-idf) [355]. Let Tf (w) be the term frequency or number of times that word w occurred in the document, and let Df (w) be the document frequency (number of documents that contain the word). Let N be the number of documents. We define T f I df ( w ) a s

TfIdf(w) = Tf(w) ∗ log N .

This is the relative importance of the word in the document, which matches our intuitive view of the importance of words. A word is more important the fewer documents it appears in (lower Df ), as well as if it ap- pears several times in a single target document (larger Tf ). Said another way, we are more interested in words that appear often in a document, but not often in the collection. Such words are intuitively more important, as they are differentiating, separating or classifying words. Figure 10.1 shows term vectors for a group of documents using tf-idf weights.

TABLE

The following pseudocode computes tf-idf vectors for each document in a given document collection. It uses the Count-Terms function in the pre- vious pseudocode example. The first section iterates through all documents, computing and storing term frequencies and document frequencies. The sec- ond section computes the tf-idf vectors for each document and stores them in a table.

Compute-TfIdf(documents)1 termF requencies ← ∅   Looks up term count tables for document names.2 documentF requencies ← ∅   Counts the documents in which a term occurs.3 uniqueT erms ← ∅   The list of all unique terms.4 for each document d in documents5 do 6789 10 11 12docName ← Name(d)   Extract the name of the document. tokenStream ← Tokenize(d)   Generate document token stream. terms ← Count-Terms(tokenStream)   Count the term frequencies. termF requencies[docN ame] ← terms   Store the term frequencies. for each term t in Keys(terms)do increment (or initialize to 1) documentFrequencies[t] uniqueT erms ← uniqueT erms ∪ t13 tfIdfV ectorTable ← ∅   Looks up tf-idf vectors for document names.14 n ← Length(documents)15 for 161718eachdodocument name docN ame in Keys(termF requencies)tfIdfVector ← create zeroed array of length Length(uniqueTerms) terms ← termF requencies[docN ame]for each term t in keys(terms)do tf ← terms[t]df ← documentF requencies[t]tfIdf ← tf ∗ log(n/df)tfIdfV ector[index of t in uniqueTerms] ← tfIdf192021222324 return tfIdfVectorTabletfIdfVe ctorTabl

###3.2. Zipf’s Law

The normal and uniform distributions are the ones we are most familiar with. The power law distribution is common today with the large data sizes we encounter, which reflect scalable phenomena. The economist Vilfredo Pareto stated that a company’s revenue is inversely proportional to its rank—a classic power law, resulting in the famous 80-20 rule, in which 20% of the population holds 80% of the wealth.

FIGURE

Harvard linguist George Kingsley Zipf stated the distribution of words in natural language corpora using a discrete power law distribution called a Zipfian distribution. Zipf’s Law [490] states that in a typical natural language document, the frequency of any word is inversely proportional to its rank in the frequency table. Plotting the Zipf curve on a log-log scale yields a straight line with a slope of −1 (see Figure 10.2).One immediate implication of Zipf’s Law is that a small number of words describe most of the key concepts in small documents. There are numerous examples of text summarization that permit a full description with just a few words.

###3.3 Tasks Using the Vector Space Model

The vector space model, when accompanied by some distance metric, allows one to perform many useful tasks. We can use tf-idf and the vector space model to identify documents of particular interest. For example, the vector space model, with the use of some distance metric, will allow us to answer

FIGURE

questions such as which documents are similar to a specific one, which doc- uments are relevant to a given collection of documents, or which documents are most relevant to a given search query—all by finding the documents whose term vectors are most similar to the given document, the average vector over a document collection, or the vector of a search query.Another indirect task is how to help the user make sense of an entire corpus. The user may be looking for patterns or for structures, such as a document’s main themes, clusters, and the distribution of themes through a document collection. This often involves visualizing the corpus in a two- dimensional layout, or presenting the user with a graph of connections be- tween documents or entities to navigate through. The visualization pipeline maps well to document visualization: we get the data (corpus), transform it into vectors, then run algorithms based on the tasks of interest (i.e., simi- larity, search, clustering), and generate the visualizations.

##4. Single Document Visualizations
Here we present several visualizations of a single text document, taken from the VAST Contest 2007 data set.

FIGURE

###Word Clouds
Word clouds (Figure 10.4), also known as text clouds or tag clouds, are layouts of raw tokens, colored and sized by their frequency within a single document. Text clouds and their variations, such as a Wordle (Figure 10.5), are examples of visualizations that use only term frequency vectors and some layout algorithm to create the visualization.

FIGURE

###WordTree
The WordTree visualization [450] is a visual representation of both term frequencies, as well as their context (Figure 10.6). Size is used to represent the term or phrase frequency. The root of the tree is a user-specified word or phrase of interest, and the branches represent the various contexts in which the word or phrase is used in the document.

FIGURE

###TextArc

We can extend the representation of word distribution by displaying con- nectivity. There are several ways in which connections can be computed. TextArc [312] is a visual representation of how terms relate to the lines of text in which they appear (Figure 10.7). Every word of the text is drawn in order around an ellipse as small lines with a slight offset at its start. As in a text cloud, more frequently occurring words are drawn larger and brighter. Words with higher frequencies are drawn within the ellipse, pulled by its oc- currences on the circle (similar to RadViz). The user is able to highlight the underlying text with probing and animate “reading” the text by visualizing the flow of the text through relevant connected terms.

FIGURE

###Arc Diagrams

Arc diagrams [451] are a visualization focused on displaying repetition in text or any sequence. Repeated subsequences are identified and connected by semicircular arcs. The thickness of the arcs represents the length of the subsequence, and the height of the arcs represents the distance between the subsequences. Figure 10.8 displays Bach’s Minuet in G Major, visualizing

FIGURE

the classic pattern of a minuet. It contains two parts, each consisting of a long passage played twice. The parts are loosely related, as shown by the bundle of thin arcs connecting the two main parts. The overlap of the two main arcs shows that the end of the first passage is the same as the beginning of the second.

###Literature Fingerprinting
Literature fingerprinting is a method of visualizing features used to char- acterize text [222]. Instead of calculating just one feature value or vector for the whole text (this is what is usually done), we calculate a sequence of feature values per text and present them to the user as a characteristic fingerprint of the document. This allows the user to “look inside” the docu- ment and analyze the development of the values across the text. Moreover, the structural information of the document is used to visualize the docu- ment on different levels of resolution. Literature fingerprinting was applied to an authorship attribution problem to show the discrimination power of the standard measures that are assumed to capture the writing style of an author (see Figure 10.9).

##5. Document Collection Visualizations
In most cases of document collection visualizations, the goal is to place sim- ilar documents close to each other and dissimilar ones far apart. This is a minimax problem and typically O(n2). We compute the similarity between all pairs of documents and determine a layout. The common approaches are graph spring layouts, multidimensional scaling, clustering (k-means, hierar- chical, expectation maximization (EM), support vector), and self-organizing maps. We present several document collection visualizations, such as self- organizing maps, cluster maps, and themescapes.

###Self-Organizing Maps

A self-organizing map (SOM) [248] is an unsupervised learning algorithm using a collection of typically 2D nodes, where documents will be located. Each node has an associated vector of the same dimensionality as the input vectors (the document vectors) used to train the map. We initialize the SOM nodes, typically with random weights. We choose a random vector from the input vectors and calculate its distance from each node. We adjust the

FIGURE

weights of the closest nodes (within a particular radius), making each closer to the input vector, with the higher weights corresponding to the closest selected node. As we iterate through the input vectors, the radius gets smaller. An example of using SOMs for text data is shown in Figure 10.10 [454], which shows a million documents collected from 83 newsgroups.

###Themescapes
Themescapes are summaries of corpora using abstract 3D landscapes in which height and color are used to represent density of similar documents. The example shown in Figure 10.11 from Pacific Northwest National Labs [407] represents news articles visualized as a themescape. The taller moun- tains represent frequent themes in the document corpus (height is propor- tional to number of documents relating to the theme).

FIGURE
FIGURE

###Document Cards
Document cards are a compact visualization (Figure 10.12) that represents the document’s key semantics as a mixture of images and important key terms, similar to cards in a top trumps game [400]. The key terms are extracted using an advanced text-mining approach based on an automatic extraction of document structure. The images and their captions are ex- tracted using a graphical heuristic, and the captions are used for a semi- semantic image weighting. Furthermore, the image color histogram is used to classify images into classes (class 1: photography/rendered image, class 2: diagram/sketch/graph, class 3: table) and show at least one representative from each non-empty class.

##6. Extended Text Visualizations
Here we investigate several text visualization techniques that involve meta- data or otherwise go beyond the typical term-vector-based visualizations.
###Software Visualization
Eick et al. developed a visualization tool called SeeSoft [108] that visualizes statistics for each line of code (i.e., age and number of modifications, pro- grammer, dates). In Figure 10.13, each column represents a source code file with the height representing the size of the file. If the file is longer than the screen, it continues into the next column. In the classic SeeSoft repre- sentation, each row represents one line of code. Since the number of lines is too large for one row, each line of code is represented by a pixel in the row. This increases the number of lines that can be displayed. Color is used to represent the call count. The more red a line is, the more often the line is called, and thus is a key hot-spot. A blue line is an infrequently called one. Color can be used to represent other parameters, such as time of last modification or number of modifications. With a 1K × 1K screen, SeeSoft is able to display up to 50,000 lines of code. This figure contains 52 files with 15,255 lines of code. The selected file is file1.c, a block of code with a zoomed-in view of line 408.

FIGURE
FIGURE

###Search Result Visualization
Marti Hearst developed a simple query result visualization foundationally similar to Keim’s pixel displays [232] called TileBars [178], which displays a number of term-related statistics, including frequency and distribution of terms, length of document, term-based ranking, and strength of ranking. Each document of the result set is represented by a rectangle, where width indicates relative length of the document and stacked squares correspond to text segments (see Figure 10.14). Each row of the stack represents a set of query terms, and the darkness of the square indicates the frequency of terms among the corresponding terms. Titles and the first words from
FIGURE

###Temporal Document Collection Visualizations
ThemeRiver [173], also called a stream graph, is a visualization of thematic changes in a document collection over time (Figure 10.15). This visualiza-

FIGURE

tion assumes that the input data progresses over time. Themes are visually represented as colored horizontal bands whose vertical thickness at a given horizontal location represents their frequency at a particular point in time.Jigsaw is a tool for visualizing and exploring text corpora [155]. Jigsaw’s calendar view positions document objects on a calendar based on date en- tities identified within the text. When the user highlights a document, the entities that occur within that document are displayed (see Figure 10.16).Wanner et al. developed a visual analytics tool for conducting semi- automatic sentiment analysis of large news feeds [440]. While the tool au- tomatically retrieves and analyzes RSS feeds with respect to positive and

FIGURE

negative opinion words, the more demanding news analysis of finding trends, spotting peculiarities, and putting events into context is left to the human expert. As shown in Figure 10.17, each single news item is represented by one visual object and plotted on a horizontal time axis according to its publication time. The shape and color of an item reveal information about the category it belongs to, and its vertical shift indicates whether it has a positive connotation (upward shift) or a negative one (downward shift)

###Representing Relationships

Jigsaw [155] also includes an entity graph view (Figure 10.18), in which the user can navigate a graph of related entities and documents. In Jigsaw, entities are connected to the documents in which they appear. The Jigsaw graph view does not show the entire document collection, but it allows the user to incrementally expand the graph by selecting documents and entities of interest (see Figure 10.19).

FIGURE
FIGURE
FIGURE

The Jigsaw list view is an alternative to the graph view in that it allows the user to explore relationships between various entity types and documents. As shown in Figure 10.20, when the user selects items of interest, the list view draws connection lines showing their relationships.

##7. Заключение
In this chapter we have explored the fundamental computational approaches to transforming unstructured text into structured data suitable for visualiza- tion and analysis. We introduced visualizations such as text clouds and word trees for finding themes and patterns within single documents. Visualiza- tions such as SOMs, map displays, and themescapes are useful for visualizing document collections. For further analysis of document collections with com- plex relationships and temporal characteristics, we briefly surveyed several visualizations, such as node graphs, ThemeRiver, and Calendar View.

##8. Что почитать


