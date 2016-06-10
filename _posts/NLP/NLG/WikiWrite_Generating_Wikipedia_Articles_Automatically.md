#WikiWrite: Generating Wikipedia Articles Automatically
##Authur
1. Siddhartha Banerjee
2. Prasenjit Mitra
##Keyword
1. WikiWrite: a system capable of generating new Wikipedia content.<b>learn content templates from similar articles without Wikipedia categories</b>
2. document embedding:文本嵌入
3. paraphrasing:释义
	1. the system used the original word without any paraphrasing.
4. Informativeness:信息量
##Abstract
1. obtains feature representations of entities on Wikipedia
	1. an existing work on document embeddings to obtain <b>vector representations</b> of words and paragraphs.(<font color="blue">Attention!Preprocessor here!</font>)
		- obtain the vector representations of <font color ="red">the red-linked entities</font> using paragraph vector model(Le and Mikolov,2014)<b>(PV-DM model)</b>
	
	2. Using words & paragraphs representation, <b>identify articles</b> that are <b>very similar to the new entity</b> on Wikipedia.
		- articles to be identified: existing Wikipedia articles that are semantically close to the red-linked entity(<font color = "blue"><b>Using cosine similarity</b></font>)
	3. Train machine learning classifiers using <b>content from the similar articles</b> to <font color = "green">assign web retrieved content on the new entity into relevant sections</font> in the new entity's Wiki.
2. Propose a novel abstractive summarization(新型抽象总结?) technique that use <b>two-step ILP model</b> to <b>synthesize the assigned content in each section</b> & rewrite the content to produce a well-formed informative summary.
	1. this Article jointly optimizes the order with the informativeness and linguistic quality of the summary(of the content assigned to the sections in the article).
	2. compute the coherence score between any two sentences using transition probabilities of word-pairs(nouns and verbs) between the sentences.
		1. <b>THE transition probabilities are learned from pairs of adjacent sentences that exist in the similar articles.</b>
	3. propose an optimization model to find a <b>suitable set of lexical and phrasal transformations</b> for <b>paraphrasing the generated summaries.</b>
##1 Introduction
###Assumption
1. Wikipedia categories are known.
	1. articles often belongs to multiple categories.
2. <font color='red'>copyright violations</font>, the text on internet can not be directly use
	1. An abstractive summarization system,use <b>sentence fusion</b>
3. sentences selected (and paraphased) from multiple docs must be ordered such that the resulting article is coherent.
	1. this Article jointly optimizes the order with the informativeness and linguistic quality of the summary(of the content assigned to the sections in the article 2.1).

###Data Source
1. obtain the red-linked entites using a paragraph vector model(Le and Mikolov,2014)
	- paragraph vector model: computes continuous distributed vector representations of varying-length texts
###How to evaluate the efficiency 
1. compare the accuracies with other comparable systems.
2. reconstruct existing articles on Wiki and compare the org & autogen
3. create 50 new articles in Wiki.
##Question
###Abstract 
1. 1.1 what's document embedding?

