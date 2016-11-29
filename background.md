#Natural Language Processing

Let's start with some definitions...

####Natural Languages
We are all very familiar with these. You speak at least one, maybe more. In natural language processing, the term 'natural language' is used to distinguish human languages from computer languages. 

Examples of natural languages include; Mandarin, English, Portuguese, Arabic -- and I bet you can name a bunch more. Examples of computer languages include Python, R, JavaScript, etc... 

Human languages come with their own histories and culture; our history and culture. They are beautiful and messy. That is why we fall in love with them. Words have connotations and multiple meanings. Languages are full of ambiguity and rules for use at difficult to pin down.  

In contrast, **artificial languages** have no such ambiguity. Computer languages are mathematical and logical. Ambiguity in computer programming languages leads to error messages. 

```---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-32-d25100ff30af> in <module>()
----> 1 love

NameError: name 'love' is not defined```

**Natural Language Processing** (NLP) tries to use programming to understand human languages. Usually, this is in the form of written text or audio that is translated into text and then converted into something the computer can understand. Numbers.  

This chapter uses NLP in a broad sense to include any computer manipulation of natural language. At one extreme, this could be simple. For example, counting word frequencies to compare different writing styles. 

Lexical density is usually a good indicator of the general tone of texts. The language of academia, for example, often has a large number of nouns to verbs. We can approximate an academic tone simply by making nominally dense clauses: 

      The consideration of interest is the potential for a participant of a certain 
      demographic to be in Group A or Group B*.

Notice how not only are there many nouns ('consideration', 'interest', 'potential', etc.), but that the verbs are very simple ('is', 'to be').

In comparison, informal speech is characterised by smaller clauses, and more verbs.

      A: Did you feel like dropping by?
      B: I thought I did, but now I don't think I want to

Here, we have only a few, simple nouns ('you', 'I'), paired with more expressive verbs ('feel', 'dropping by', 'think', 'want').

At the other extreme, you can get very complicated very quickly with NLP. For example, 'understanding' complete human utterances to the extent that a computer can be program to respond. You may have experienced this technology through an automated phone dialogue system and perhaps encountered a certain level of frustration at the limits of the technology to date. This chapter will not approach to level of complication and will stick with analysis of written texts. 





