#Background

Let's start with some definitions...

##Natural Languages:
We are all very familiar with these. You speak at least one, maybe more. In natural language processing we use the slightly strange term 'natural language' to distinguish human languages from computer languages. 

Some examples of natural languages include; Mandarin, English, Portuguese, Arabic -- and I bet you can name a bunch more. 

These languages come with their own histories and culture; our history and culture. They are beautiful and messy. That's why we fall in love with them. Languages are full of ambiguity and mystery and words have multiple meanings.  


In contrast, **artificial languages**, for example Python, have no such ambiguity. Computer languages are mathematical and logical. Ambiguity in computer programming languages leads to error messages. 

```---------------------------------------------------------------------------
NameError                                 Traceback (most recent call last)
<ipython-input-32-d25100ff30af> in <module>()
----> 1 love

NameError: name 'love' is not defined```

**Natural Language Processing** (NLP) tries to use programming to understand human languages. Usually, this is in the form of written text or audio that is translated into text and then converting language into something the computer can understand. Numbers.  

I am using NLP in a broad sense here... i.e. any computer manipulation of natural language. 

At one extreme, this could be simple. For example, counting word frequencies to compare different writing styles. 

Lexical density is usually a good indicator of the general tone of texts. The language of academia, for example, often has a huge number of nouns to verbs. We can approximate an academic tone simply by making nominally dense clauses: 

      The consideration of interest is the potential for a participant of a certain 
      demographic to be in Group A or Group B*.

Notice how not only are there many nouns (*consideration*, *interest*, *potential*, etc.), but that the verbs are very simple (*is*, *to be*).

In comparison, informal speech is characterised by smaller clauses, and thus more verbs.

      A: Did you feel like dropping by?
      B: I thought I did, but now I don't think I want to

Here, we have only a few, simple nouns (*you*, *I*), with more expressive verbs (*feel*, *dropping by*, *think*, *want*).

At the other extreme, you can get very complicated very quickly. For example, "understanding" complete human utterances to the extend you can respond to them.

!!--get an example of a complicated nlp project, preferably a visual and relatable one--!!



