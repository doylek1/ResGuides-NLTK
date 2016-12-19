#Natural Language Processing

Let's start with some definitions...

####Natural Languages
We are all very familiar with natural languages. You speak at least one, maybe more. In natural language processing, the term 'natural language' is used to distinguish human languages from computer languages. 

Examples of natural languages include; Mandarin, English, Portuguese, Arabic — and I bet you can name a bunch more. 

Human languages come with their own histories and culture; think about your own history and culture. These languages are beautiful and messy. That is why we fall in love with them. Words have connotations and multiple meanings. Languages are full of ambiguity and rules for use can be difficult to pin down.  

####Computer languages
In contrast, artificial languages have no such ambiguity. Computer languages are mathematical and logical. Ambiguity in computer programming languages leads to error messages. 

```---------------------------------------------------------------------------
1 love

NameError: name 'love' is not defined```

Examples of computer languages you might have heard of (some covered in this book) include Python, R, Matlab, and JavaScript.

####Natural Language Processing (NLP) 
NLP uses programming to understand human languages. Usually, this is in the form of written text or audio that is translated into text and then converted into something the computer can understand... Numbers.  

This chapter uses the term NLP in a broad sense to include any computer manipulation of natural language. A simple example is: counting word frequencies to compare different writing styles. 

####An example...

Lexical density - calculated as the number of lexical words (nouns, verbs, adjectives, etc) in a text divided by the total number of words - is usually a good indicator of the general tone of texts. The language of academia, for example, often has a large number of nouns to verbs. We can approximate an academic tone simply by making nominally dense clauses: 

      The consideration of interest is the potential for a participant of a certain 
      demographic to be in Group A or Group B.

Notice how not only are there many nouns ('consideration', 'interest', 'potential', etc.), but that the verbs are very simple ('is', 'to be').

In comparison, informal speech is characterised by smaller clauses, and more verbs.

      A: Did you feel like dropping by?
      B: I thought I did, but now I don't think I want to.

Here, we have only a few, simple nouns ('you', 'I'), paired with more expressive verbs ('feel', 'dropping by', 'think', 'want').

NLP also has the potential to get very complicated very quickly. For example, 'understanding' complete human utterances to the extent that a computer can be programmed to sensibly respond. You may have experienced this technology through an automated phone dialogue system and perhaps encountered a certain level of frustration at the limits of the technology to date. Don't worry, this chapter won't approach this level of complication and will stick with analysis of written texts! 





