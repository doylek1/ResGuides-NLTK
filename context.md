# The Natural Language Toolkit
NLTK is a Python Library for working with written language data. It is free, open source and [well documented](http://www.nltk.org/). 
> Note: NLTK provides tools for tasks ranging from very simple (counting words in a text) to very complex (writing and training parsers, etc.). Many advanced tasks are beyond the scope of this chapter

Many areas covered in this chapter are covered in more detail in the [NLTK Book](http://www.nltk.org/book/). Some of the tasks NLTK can help you with include; tokenization (turning words in discrete data), stemming (removal of derivational affixes e.g. 's' 'ed', 'ing'), tagging (with parts-of-speech, for e.g) and parsing (creating a parse tree, for e.g.). The example below is a parse tree, which includes parts-of-speech tags (S = sentence, NN = noun, etc...).

![](images/tree.gif)
(Figure 1. Parse tree, Bird et al. 2009)

The data we will be working with for the activity has already had some processing done on them so that we could use NLTK to find features of the language. However, Python regards a text file as a single long string of characters. The first thing to do is to start breaking the text up into sentences and words. Here is an example of one of NLTK's tokenizers at work:

```python
sentence = "They refuse to permit us the refuse permit"
words = word_tokenize(sentence)
tagged = nltk.pos_tag(words, tagset='universal')
print(tagged)
```

    [('They', u'PRON'), ('refuse', u'VERB'), ('to', u'PRT'), ('permit', u'VERB'), ('us', u'PRON'), ('the', u'DET'), ('refuse', u'NOUN'), ('permit', u'NOUN')]


Part of Speech tagging creates bigrams, that is, it associates the word with its tag in a pair of items that we can see above in brackets.  

NLTK began its life in 2001 as a project of Steven Bird and Edward Loper. At the time, Bird was a professor in computational linguistics at the University of Pennsylvania and Loper, his star student. Together they agreed a plan for developing software infrastructure for NLP teaching that could be easily maintained over time. 

That software infrastructure became NLTK. The toolkit supports at least 40 different languages and is now used in university courses around the world. The book *Natural Language Processing with Python* (2009), written by Steven Bird, Edward Loper and their collaborator Ewan Klein, has been cited at least 461 times. This literature covers the gamut of disciplines, from computer science to the social sciences, engineering, mathematics, medicine, biochemistry and genetics to business, management and accounting, to name only a few. 