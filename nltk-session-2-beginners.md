
<br>
<img style="float:left" src="http://ipython.org/_static/IPy_header.png" />
<br>

# Session 2: Loading text, tokenisation, tagging, dictionaries and ngrams


```python
from __future__ import print_function, division

import sys
import nltk
from IPython.display import display, clear_output
sys.path.append("/usr/lib/python2.7/site-packages/")
%matplotlib inline
```


```python
from nltk.book import *
```

**Welcome back!**

So, what did we learn yesterday? A brief recap:

* The **IPython** Notebook
* **Python**: syntax, variables, functions, etc.

Today's focus will be on **developing more advanced NLTK skills** and using these skills to **investigate our own data**. 

*Any questions or anything before we dive in?*

## Uploading text files

First of all, let's load in our text.

Google the Gutenberg Project and download a book as a plain text file. 

I chose [A Modest Proposal](https://www.gutenberg.org/ebooks/1080)

We can also look at file contents within the IPython Notebook itself:


```python
import os
```


```python
# import tokenizers
from nltk import word_tokenize
from nltk.text import Text
```


```python
text_path = '/home/researcher/modest_proposal.txt'
```


```python
file = open(os.path.join(text_path), "r", encoding='UTF-8')
text = file.read()
print(text[749:2000])
```

    MODEST PROPOSAL
    
    For preventing the children of poor people in Ireland, from being a
    burden on their parents or country, and for making them beneficial to
    the publick.
    
    by Dr. Jonathan Swift
    
    
    1729
    
    
    
    It is a melancholy object to those, who walk through this great town,
    or travel in the country, when they see the streets, the roads and
    cabbin-doors crowded with beggars of the female sex, followed by three,
    four, or six children, all in rags, and importuning every passenger for
    an alms. These mothers instead of being able to work for their honest
    livelihood, are forced to employ all their time in stroling to beg
    sustenance for their helpless infants who, as they grow up, either turn
    thieves for want of work, or leave their dear native country, to fight
    for the Pretender in Spain, or sell themselves to the Barbadoes.
    
    I think it is agreed by all parties, that this prodigious number of
    children in the arms, or on the backs, or at the heels of their mothers,
    and frequently of their fathers, is in the present deplorable state of
    the kingdom, a very great additional grievance; and therefore whoever
    could find out a fair, cheap and easy method of making these children
    sound and useful members of the common-wealth, would deserve so well of


The books were were working with yesterday had already had some processing done on them so that we could use NLTK to find features of the language. Remember that Python regards a text file as a single long string of characters. The first thing to do is to start breaking the text up into sentences and words.


```python
from nltk import word_tokenize
text = open('/home/researcher/modest_proposal.txt', "r", encoding='UTF-8').read() 
tokens = word_tokenize(text)
print(tokens[:100])
```

    ['\ufeffThe', 'Project', 'Gutenberg', 'EBook', 'of', 'A', 'Modest', 'Proposal', ',', 'by', 'Jonathan', 'Swift', 'This', 'eBook', 'is', 'for', 'the', 'use', 'of', 'anyone', 'anywhere', 'at', 'no', 'cost', 'and', 'with', 'almost', 'no', 'restrictions', 'whatsoever', '.', 'You', 'may', 'copy', 'it', ',', 'give', 'it', 'away', 'or', 're-use', 'it', 'under', 'the', 'terms', 'of', 'the', 'Project', 'Gutenberg', 'License', 'included', 'with', 'this', 'eBook', 'or', 'online', 'at', 'www.gutenberg.org', 'Title', ':', 'A', 'Modest', 'Proposal', 'For', 'preventing', 'the', 'children', 'of', 'poor', 'people', 'in', 'Ireland', ',', 'from', 'being', 'a', 'burden', 'on', 'their', 'parents', 'or', 'country', ',', 'and', 'for', 'making', 'them', 'beneficial', 'to', 'the', 'publick', '-', '1729', 'Author', ':', 'Jonathan', 'Swift', 'Posting', 'Date', ':']


**Challenge!**

1. Find a .txt file from the Gutenberg Project or elsewhere and upload it to the Jupyter Notebook. 
2. Use the word_tokenize to break up the text data. 
3. Print the first 100 tokens.

Breaking a speech into tokens lets us do the sort of word counting that we were doing yesterday on the speeches. We can do some more interesting linguistic analysis if we use Part of Speech tagging. NLTK has a number of different Part of Speech tags that we could use, but the simplest one is called 'Universal', and we'll use that here.


```python
sentence = "They refuse to permit us the refuse permit"
words = word_tokenize(sentence)
tagged = nltk.pos_tag(words, tagset='universal')
print(tagged)
```

    [('They', u'PRON'), ('refuse', u'VERB'), ('to', u'PRT'), ('permit', u'VERB'), ('us', u'PRON'), ('the', u'DET'), ('refuse', u'NOUN'), ('permit', u'NOUN')]


Part of Speech tagging creates bigrams, that is, it associates the word with its tag in a pair of items that we can see above in brackets.  


```python
tag_fd = nltk.FreqDist(tag for (word, tag) in tagged)
tag_fd.most_common()
```




    [(u'PRON', 2), (u'VERB', 2), (u'NOUN', 2), (u'DET', 1), (u'PRT', 1)]



**Challenge!**

Use Part of Speech tagging to tag the text that we have just tokenised the do the following:
* Find the most common parts of speech
* Find the most common verbs and create a frequency Distribution graph of your result
* Find the 10 most common nouns in the text

*Hint: to find the most common verbs and nouns, you will need to create a list that contains only the verbs or only the nouns from the speech. Use a for loop to create your list. Then create a frequency distribution*


```python
tagged_text = nltk.pos_tag(tokens, tagset = 'universal')
text_fd = nltk.FreqDist(tag for (word, tag) in tagged_text)
text_fd.most_common()
```




    [('NOUN', 1871),
     ('VERB', 1082),
     ('ADP', 905),
     ('.', 846),
     ('DET', 751),
     ('ADJ', 503),
     ('PRON', 399),
     ('CONJ', 314),
     ('ADV', 296),
     ('PRT', 208),
     ('NUM', 129)]




```python
verblist = []
for (word, tag) in tagged_text:
    if tag == 'VERB':
        verblist.append(word)
# Check the length of the list of verbs. 
#If it matches the number of verbs above, you can be fairly sure your loop has worked as expected
print(len(verblist))
verb_fd = nltk.FreqDist(verblist)
print(verb_fd.most_common()[:10])
```

    1082
    [('be', 67), ('is', 47), ('are', 41), ('will', 41), ('have', 33), ('can', 29), ('may', 26), ('would', 18), ('being', 17), ('do', 16)]



```python
nounlist = []
for (word, tag) in tagged_text:
    if tag == 'NOUN':
        nounlist.append(word)
print(nounlist[:10])
print(len(nounlist))
noun_fd = nltk.FreqDist(nounlist)
print(noun_fd.most_common()[:10])
```

    ['Project', 'Gutenberg', 'EBook', 'A', 'Modest', 'Proposal', 'Jonathan', 'Swift', 'eBook', 'use']
    1871
    [('Project', 80), ('Gutenberg-tm', 55), ('work', 49), ('works', 30), ('Gutenberg', 27), ('Foundation', 24), ('children', 20), ('terms', 19), ('agreement', 17), ('country', 16)]


**Extension**
There are a few things to note about this result - Project and Gutenberg have been returned as two different, very frequent nouns. Because we're humans, not computers, we know it's likely that they are often occuring together. We could test for bigrams (words that typically occur side by side) to see if this is the case. 

In order to perform this test, we must first convert our list of tokens into and NLTK text. We can then use specific NLTK functions on the text.


```python
print(type(tokens))
nltk_text = nltk.Text(tokens)
print(type(nltk_text))
nltk_text.collocations()
```

    <class 'list'>
    <class 'nltk.text.Text'>
    Project Gutenberg-tm; Project Gutenberg; Literary Archive; Archive
    Foundation; Gutenberg Literary; United States; Gutenberg-tm
    electronic; electronic works; set forth; public domain; electronic
    work; Gutenberg-tm License; Jonathan Swift; per annum; copyright
    holder; MODEST PROPOSAL; Modest Proposal; PROJECT GUTENBERG; twenty
    thousand; year old


### Some linguistics...

*Functional linguistics* is a research area concerned with how *realised language* (lexis and grammar) work to achieve meaningful social functions.

One functional linguistic theory is *Systemic Functional Linguistics*, developed by Michael Halliday (Prof. Emeritus at University of Sydney).

Central to the theory is a division between **experiential meanings** and **interpersonal meanings**.

* Experiential meanings communicate what happened to whom, under what circumstances.
* Interpersonal meanings negotiate identities and role relationships between speakers 

Halliday argues that these two kinds of meaning are realised **simultaneously** through different parts of English grammar.

* Experiential meanings are made through **transitivity choices**.
* Interpersonal meanings are made through **mood choices**


Transitivity choices include fitting together configurations of:

* Participants (*a man, green bikes*)
* Processes (*sleep, has always been, is considering*)
* Circumstances (*on the weekend*, *in Australia*)

Mood features of a language include:

* Mood types (*declarative, interrogative, imperative*)
* Modality (*would, can, might*)
* Lexical density--wordshe number of words per clause, the number of content to non-content words, etc.

Lexical density is usually a good indicator of the general tone of texts. The language of academia, for example, often has a huge number of nouns to verbs. We can approximate an academic tone simply by making nominally dense clauses: 

      The consideration of interest is the potential for a participant of a certain demographic to be in Group A or Group B*.

Notice how not only are there many nouns (*consideration*, *interest*, *potential*, etc.), but that the verbs are very simple (*is*, *to be*).

In comparison, informal speech is characterised by smaller clauses, and thus more verbs.

      A: Did you feel like dropping by?
      B: I thought I did, but now I don't think I want to

Here, we have only a few, simple nouns (*you*, *I*), with more expressive verbs (*feel*, *dropping by*, *think*, *want*)

> **Note**: SFL argues that through *grammatical metaphor*, one linguistic feature can stand in for another. *Would you please shut the door?* is an interrogative, but it functions as a command. *invitation* is a nominalisation of a process, *invite*. We don't have time to deal with these kinds of realisations, unfortunately.

In the context of Fraser's speech, there are nearly twice as many nouns as verbs, and the verbs are generally quite simple ones (parts of To Be and To Have make up about a quarter). This suggests that Fraser's speech, even when giving a radio talk to his electorate, is more towards the formal end of the spectrum. 

## Recap
So far today we have:
* Imported text into NLTK
* Tokenised raw text into words
* Tagged words as parts of speech
* Converted a list into NLTK Text for further analysis

## Stopwords
Yesterday, when we did our frequency counts of the books in the NLTK Library, we noticed that a lot of speace was taken up by little words like 'and' and 'of' and 'the' which don't add a lot to our understanding of text. These are called 'stop words'. It will help our analysis if we exclude them.


```python
fdist1 = nltk.FreqDist(tokens)
fdist1.most_common()[:20]
```




    [(',', 510),
     ('the', 327),
     ('of', 236),
     ('.', 183),
     ('to', 182),
     ('and', 177),
     ('a', 141),
     ('in', 125),
     ('or', 106),
     ('Project', 83),
     ('be', 67),
     ('for', 63),
     ('this', 60),
     ('with', 58),
     ('by', 55),
     ('Gutenberg-tm', 55),
     ('I', 55),
     ('you', 52),
     ('that', 51),
     ('work', 50)]




```python
print(len(nltk_text))
print(len(set(nltk_text)))
```

    7304
    1795



```python
#First let's get rid of the puncutation
text = [word for word in nltk_text if word.isalpha()]
print(len(text))#Then get rid of capitals
vocab = [word.lower() for word in text]
print(len(set(vocab)))
```

    6273
    1551



```python
from nltk.corpus import stopwords
#Create a variable that contains all the stopwords in the NLTK corpus
ignored_words = nltk.corpus.stopwords.words('english')
unstopped = [word for word in vocab if word not in stopwords.words('english')]
fdist2 = nltk.FreqDist(unstopped)
fdist2.most_common()[:20]
```




    [('project', 88),
     ('work', 51),
     ('works', 32),
     ('gutenberg', 30),
     ('electronic', 27),
     ('may', 26),
     ('foundation', 25),
     ('terms', 21),
     ('children', 20),
     ('agreement', 18),
     ('would', 18),
     ('one', 17),
     ('country', 16),
     ('thousand', 15),
     ('kingdom', 15),
     ('donations', 15),
     ('upon', 15),
     ('license', 15),
     ('states', 14),
     ('number', 14)]



The list we have now is probably more intersting if we wanted to get a sense of the key issues in the text. Note, we're working with a very small sample here. This sort of analysis is much more useful over really big corpora.

*Note: We could have condensed the first two steps into a single line of code that looked like this:*

        unstopped = [word for word in speech if word.lower() not in stopwords.words('english') and word.isalpha()]

## Collocation
We've just used collocation to test a hypothesis about the most common nouns in the speech we were investigating. Collocation can be quite a powerful tool for finding features of language.

First, let's look for bigrams in the whole list of tokens:


```python
from nltk.collocations import *
bigram_measures = nltk.collocations.BigramAssocMeasures()
finder = BigramCollocationFinder.from_words(tokens)
sorted(finder.nbest(bigram_measures.raw_freq, 10))
```




    [(',', 'and'),
     (',', 'or'),
     (',', 'that'),
     (',', 'the'),
     ('Project', 'Gutenberg'),
     ('Project', 'Gutenberg-tm'),
     ('in', 'the'),
     ('of', 'the'),
     ('the', 'Project'),
     ('to', 'the')]



That doesn't tell us much. Let's try again with 'unstopped' our list of tokens with the punctuation and stopwords removed


```python
from nltk.collocations import *
bigram_measures = nltk.collocations.BigramAssocMeasures()
finder = BigramCollocationFinder.from_words(unstopped)
sorted(finder.nbest(bigram_measures.raw_freq, 10))
```




    [('archive', 'foundation'),
     ('electronic', 'work'),
     ('electronic', 'works'),
     ('gutenberg', 'literary'),
     ('literary', 'archive'),
     ('project', 'electronic'),
     ('project', 'gutenberg'),
     ('project', 'license'),
     ('terms', 'agreement'),
     ('united', 'states')]



As well as identifying collocations (words that appear near each other), we can also look for n-grams or clusters, which appear immediately adjacent to each other. Repeated N-grams are a good way to get a sense of what a text is about. First, let's see how n-grams are created:


```python
print(sent2)
```

    ['The', 'family', 'of', 'Dashwood', 'had', 'long', 'been', 'settled', 'in', 'Sussex', '.']



```python
from nltk.util import ngrams
trigrams = ngrams(sent2, 3)
for gram in trigrams:
    print(gram)
```

    ('The', 'family', 'of')
    ('family', 'of', 'Dashwood')
    ('of', 'Dashwood', 'had')
    ('Dashwood', 'had', 'long')
    ('had', 'long', 'been')
    ('long', 'been', 'settled')
    ('been', 'settled', 'in')
    ('settled', 'in', 'Sussex')
    ('in', 'Sussex', '.')


There are a lot of trigrams in the sentence, and they don't tell us much. It's when n-grams are repeated that they start to get interesting, but before we write code the code for that we need to have some knowledge of dictionaries...

### Building a dictionaries

We've already worked with strings and lists. Another kind of data structure in Python is a dictionary.
Here is how a simple dictionary works:


```python
# create a dictionary
commonwords = {'the': 4023, 'of': 3809, 'a': 3098}
# search the dictionary for 'of'
commonwords['of']
```




    3809




```python
type(commonwords)
```




    dict



The point of dictionaries is to store a key (the word) and a value (the count). When you ask for the key, you get its value.

Notice that you use curly braces for dictionaries, but square brackets for lists.

### Finding duplicate ngrams


```python
import operator
from collections import Counter
threshold = 2
ng = 3
testtext = tokens

#Create out ngram, convert to a list, 
#run a counter to count the number of entries for each unique list element
raw_grams = ngrams(testtext, ng)
listgrams = list(raw_grams)
counts = Counter(listgrams)
print(len(listgrams), len(counts))
#Create a regular dictionary, this is mostly done so we can ignore Counter values less than threshold
D = {}
for k,v in counts.items():
    if v > threshold:
        D[k] = v
#Here is a way to sort a dictionary, based on the value (key=operator.itemgetter(1))
sorted_x = sorted(D.items(), key=operator.itemgetter(1), reverse=True)
```

    7302 6540



```python
sorted_x
```




    [(('Project', 'Gutenberg-tm', 'electronic'), 18),
     (('the', 'Project', 'Gutenberg'), 15),
     (('Project', 'Gutenberg', 'Literary'), 13),
     (('Gutenberg', 'Literary', 'Archive'), 13),
     (('Literary', 'Archive', 'Foundation'), 13),
     (('Gutenberg-tm', 'electronic', 'works'), 12),
     (('the', 'Project', 'Gutenberg-tm'), 12),
     (('the', 'terms', 'of'), 12),
     (('terms', 'of', 'this'), 10),
     (('of', 'this', 'agreement'), 10),
     (('the', 'United', 'States'), 9),
     (('set', 'forth', 'in'), 8),
     (('.', 'If', 'you'), 8),
     (('of', 'Project', 'Gutenberg-tm'), 8),
     (('Project', 'Gutenberg-tm', 'License'), 8),
     (('of', 'the', 'Project'), 8),
     (('to', 'the', 'Project'), 7),
     (('Gutenberg-tm', 'electronic', 'work'), 6),
     (('this', 'agreement', ','), 6),
     (('terms', 'of', 'the'), 5),
     ((',', 'you', 'must'), 5),
     (('.', 'You', 'may'), 5),
     (('Project', 'Gutenberg', "''"), 5),
     (('``', 'Project', 'Gutenberg'), 5),
     (('.', 'I', 'have'), 5),
     (('full', 'Project', 'Gutenberg-tm'), 5),
     (('in', 'the', 'United'), 5),
     (('a', 'Project', 'Gutenberg-tm'), 5),
     (('the', 'number', 'of'), 5),
     (('Project', 'Gutenberg-tm', 'works'), 5),
     (('Project', 'Gutenberg-tm', 'work'), 5),
     (('the', 'phrase', '``'), 4),
     (('Project', 'Gutenberg-tm', 'trademark'), 4),
     (('phrase', '``', 'Project'), 4),
     (('United', 'States', '.'), 4),
     (('the', 'copyright', 'holder'), 4),
     (('.', 'The', 'Foundation'), 4),
     (('the', 'full', 'Project'), 4),
     ((',', 'as', 'they'), 4),
     ((',', 'who', 'are'), 4),
     ((',', 'and', 'the'), 4),
     (('part', 'of', 'this'), 4),
     (('can', 'not', 'be'), 4),
     (('of', 'the', 'kingdom'), 4),
     (('or', 'any', 'other'), 4),
     (('the', 'use', 'of'), 4),
     (('at', 'http', ':'), 4),
     (('outside', 'the', 'United'), 3),
     ((',', 'as', 'I'), 3),
     (('If', 'an', 'individual'), 3),
     ((',', 'or', 'any'), 3),
     (('not', 'agree', 'to'), 3),
     (('as', 'set', 'forth'), 3),
     (('of', 'the', 'copyright'), 3),
     (('a', 'year', 'old'), 3),
     (('of', 'the', 'work'), 3),
     (('paragraph', '1.F.3', ','), 3),
     (('at', 'a', 'year'), 3),
     (('you', 'do', 'not'), 3),
     (('(', 'c', ')'), 3),
     (('.', 'Information', 'about'), 3),
     (('work', ',', 'or'), 3),
     (('the', 'owner', 'of'), 3),
     (('of', 'electronic', 'works'), 3),
     (('for', 'the', 'use'), 3),
     (('agreement', ',', 'you'), 3),
     ((',', 'and', 'for'), 3),
     (('received', 'the', 'work'), 3),
     (('free', 'distribution', 'of'), 3),
     (('by', 'all', 'the'), 3),
     (('year', 'old', ','), 3),
     (('.', 'If', 'an'), 3),
     ((',', 'that', 'a'), 3),
     (('you', 'received', 'the'), 3),
     (('this', 'kingdom', ','), 3),
     ((',', 'in', 'the'), 3),
     (('owner', 'of', 'the'), 3),
     (('this', 'electronic', 'work'), 3),
     (('A', 'MODEST', 'PROPOSAL'), 3),
     (('.', 'Do', 'not'), 3),
     (('electronic', 'work', 'is'), 3),
     (('I', 'have', 'already'), 3),
     (('permission', 'of', 'the'), 3),
     (('A', 'Modest', 'Proposal'), 3),
     (('children', 'of', 'poor'), 3),
     (('person', 'or', 'entity'), 3),
     (('of', 'poor', 'people'), 3),
     (('the', 'publick', ','), 3),
     (('electronic', 'works', '.'), 3),
     ((',', 'which', ','), 3),
     (('which', ',', 'as'), 3),
     (('forth', 'in', 'paragraph'), 3),
     (('you', 'can', 'do'), 3),
     (('any', 'Project', 'Gutenberg-tm'), 3),
     (('the', 'kingdom', ','), 3),
     (('can', 'do', 'with'), 3),
     (('to', 'the', 'publick'), 3),
     (('electronic', 'works', 'in'), 3),
     (('electronic', 'work', ','), 3),
     (('as', 'I', 'have'), 3),
     (('country', ',', 'and'), 3),
     (('The', 'Project', 'Gutenberg'), 3),
     (('years', 'old', ','), 3),
     ((';', 'and', 'I'), 3),
     ((',', 'as', 'to'), 3),
     ((',', 'performing', ','), 3),
     (('the', 'charge', 'of'), 3),
     (('all', 'the', 'terms'), 3),
     (('the', 'public', 'domain'), 3),
     (('I', 'have', 'been'), 3),
     (('electronic', 'works', ','), 3),
     ((',', 'and', 'therefore'), 3),
     (('per', 'annum', ','), 3),
     (('or', 'online', 'at'), 3),
     (('copies', 'of', 'Project'), 3),
     (('the', 'children', 'of'), 3),
     (('as', 'to', 'the'), 3),
     (('complying', 'with', 'the'), 3)]



This last bit of code is more advanced. Don't worry if you forget what every line means. If you are interested getting more comfortable with Python, come to our [Python]('https://github.com/resbaz/2015-12-14-Python-for-Researchers') course.

# Web scraping using Beautiful Soup

The most important skill for using NLTK in your life as a researchers is going to be working with your own texts. First, let's look at reading in text files directly from the web.

Of course, a lot of the text you're going to want to work with won't be in handy text files already. That's where a Python library called Beautiful Soup comes in.

*Note*: the ! is a way of accessing command line functions from the notebook. We could also do this in the terminal (without the !). 


```python
!sudo pip3 install BeautifulSoup4
from urllib.request import urlopen
```

    Requirement already satisfied (use --upgrade to upgrade): BeautifulSoup4 in /usr/local/lib/python3.4/dist-packages
    Cleaning up...



```python
from bs4 import BeautifulSoup
```


```python
url = "http://en.wikipedia.org/wiki/Smog"
```


```python
raw = urlopen(url).read()
print(type(raw))
print(raw[100:200])
```

    <class 'bytes'>
    b'>Smog - Wikipedia, the free encyclopedia</title>\n<script>document.documentElement.className = docume'


Beautiful Soup breaks the single long string into its constituent parts, creating an object 'Beautiful Soup'


```python
soup = BeautifulSoup(raw, 'html.parser')
print(type(soup))
```

    <class 'bs4.BeautifulSoup'>



```python
texts = []
for para in soup.find_all('p'):
    text = para.text
    texts.append(text)
print(texts[:10])
```

    ['Smog is a type of air pollutant. The word "smog" was coined in the early 20th century as a portmanteau of the words smoke and fog to refer to smoky fog.[1] The word was then intended to refer to what was sometimes known as pea soup fog, a familiar and serious problem in London from the 19th century to the mid 20th century. This kind of visible air pollution is composed of nitrogen oxides, sulfur oxides, ozone, smoke or particulates among others (less visible pollutants include carbon monoxide, CFCs and radioactive sources). Man-made smog is derived from coal emissions, vehicular emissions, industrial emissions, forest and agricultural fires and photochemical reactions of these emissions.', 'Modern smog, as found for example in Los Angeles, is a type of air pollution derived from vehicular emission from internal combustion engines and industrial fumes that react in the atmosphere with sunlight to form secondary pollutants that also combine with the primary emissions to form photochemical smog. In certain other cities, such as Delhi, smog severity is often aggravated by stubble burning in neighboring agricultural areas. The atmospheric pollution levels of Los Angeles, Beijing, Delhi, Mexico City, Tehran and other cities are increased by inversion that traps pollution close to the ground. It is usually highly toxic to humans and can cause severe sickness, shortened life or death.', '', '', 'Coinage of the term "smog" is generally attributed to Dr. Henry Antoine Des Voeux in his 1905 paper, "Fog and Smoke" for a meeting of the Public Health Congress. The July 26, 1905 edition of the London newspaper Daily Graphic quoted Des Voeux, "He said it required no science to see that there was something produced in great cities which was not found in the country, and that was smoky fog, or what was known as \'smog.\'"[2] The following day the newspaper stated that "Dr. Des Voeux did a public service in coining a new word for the London fog." However, this is predated by a Los Angeles Times article of January 19, 1893, in which the word is attributed to "a witty English writer."', "Coal fires, used to heat individual buildings or in a power-producing plant, can emit significant clouds of smoke that contributes to smog. Air pollution from this source has been reported in England since the Middle Ages.[3] London, in particular, was notorious up through the mid-20th century for its coal-caused smogs, which were nicknamed 'pea-soupers.' Air pollution of this type is still a problem in areas that generate significant smoke from burning coal, as witnessed by the 2013 autumnal smog in Harbin, China, which closed roads, schools, and the airport.", 'Traffic emissions – such as from trucks, buses, and automobiles – also contribute.[4] Airborne by-products from vehicle exhaust systems cause air pollution and are a major ingredient in the creation of smog in some large cities.[5][6][7][8]', 'The major culprits from transportation sources are carbon monoxide (CO),[9][10] nitrogen oxides (NO and NOx),[11][12][13] volatile organic compounds,[10][11] sulfur dioxide,[10] and hydrocarbons.[10] (Hydrocarbons are the main components of petroleum fuels such as gasoline and diesel fuel.) These molecules react with sunlight, heat, ammonia, moisture, and other compounds to form the noxious vapors, ground level ozone, and particles that comprise smog.[10][11]', 'Photochemical smog is the chemical reaction of sunlight, nitrogen oxides and volatile organic compounds in the atmosphere, which leaves airborne particles and ground-level ozone.[14] This noxious mixture of air pollutants may include the following:', 'A primary pollutant is an air pollutant emitted directly from a source. A secondary pollutant is not directly emitted as such, but forms when other pollutants (primary pollutants) react in the atmosphere. Examples of a secondary pollutant include ozone, which is formed when hydrocarbons (HC) and nitrogen oxides (NOx) combine in the presence of sunlight; nitrogen dioxide (NO2), which is formed as nitric oxide (NO) combines with oxygen in the air; and acid rain, which is formed when sulfur dioxide or nitrogen oxides react with water.[15] All of these harsh chemicals are usually highly reactive and oxidizing. Photochemical smog is therefore considered to be a problem of modern industrialization. It is present in all modern cities, but it is more common in cities with sunny, warm, dry climates and a large number of motor vehicles.[16] Because it travels with the wind, it can affect sparsely populated areas as well.']



```python
import re
regex = re.compile('\[[0-9]*\]')
joined_texts = '\n'.join(texts)
joined_texts = re.sub(regex, '', joined_texts)
print(type(joined_texts))
print(joined_texts[:100])
```

    <class 'str'>
    Smog is a type of air pollutant. The word "smog" was coined in the early 20th century as a portmante


In order to work on the text, the first step is to tokenise it into words.


```python
import nltk
wordlist = nltk.word_tokenize(joined_texts)
wordlist[:8]
```




    ['Smog', 'is', 'a', 'type', 'of', 'air', 'pollutant', '.']



For some other types of analysis, we'll need to create an NLTK text object


```python
good_text = nltk.Text(wordlist)
good_text.concordance('smog')
```

    Displaying 25 of 39 matches:
                                         Smog is a type of air pollutant . The wor
                                         smog '' was coined in the early 20th cent
    and radioactive sources ) . Man-made smog is derived from coal emissions , veh
    eactions of these emissions . Modern smog , as found for example in Los Angele
    mary emissions to form photochemical smog . In certain other cities , such as 
    rtain other cities , such as Delhi , smog severity is often aggravated by stub
    fe or death . Coinage of the term `` smog '' is generally attributed to Dr. He
     clouds of smoke that contributes to smog . Air pollution from this source has
     , as witnessed by the 2013 autumnal smog in Harbin , China , which closed roa
     major ingredient in the creation of smog in some large cities . The major cul
     ozone , and particles that comprise smog . Photochemical smog is the chemical
    s that comprise smog . Photochemical smog is the chemical reaction of sunlight
    active and oxidizing . Photochemical smog is therefore considered to be a prob
    automotive exhaust and photochemical smog was discovered in the 1950s by Arie 
    wo key components to the creation of smog . However , the smog created as a re
    the creation of smog . However , the smog created as a result of a volcanic er
    s been linked to the distribution of smog in some areas . For example , the cr
     has been shown to have an effect on smog distribution that is more than fossi
     than fossil fuel combustion alone . Smog is a serious problem in many cities 
    o Medical Association announced that smog is responsible for an estimated 9,50
     who had healthy babies , found that smog in the San Joaquin Valley area of Ca
    w the current accepted safe levels . Smog can form in almost any climate where
    hi 's children and women . The dense smog in Delhi during winter season result
    results in severe intensification of smog over Delhi . The state government of
    ust our iron . '' Severe episodes of smog continued in the 19th and 20th centu


And once we've done all that work creating clean text, it's a good idea to save it for later.


```python
%cd
! mkdir smog
%cd smog
```

    /home/researcher
    mkdir: cannot create directory 'smog': File exists
    /home/researcher/smog



```python
NLTK_file = open("NLTK-Smog.txt", "w", encoding='UTF-8')
NLTK_file.write(str(wordlist))
NLTK_file.close()
```


```python
text_file = open("Smog-text.txt", "w", encoding='UTF-8')
text_file.write(joined_texts)
text_file.close()
```


```python
joined_texts[2450:2471]
```




    'of this type is still'




```python
#joined_texts[2450:2470]
text_file = open("Smog-text.txt", "w", encoding='UTF-8')
text_file.write(joined_texts)
text_file.close()
```

Now have a look at the two files you've created in the file management system. Open them. How is the nltk file different from the .txt file?

**Challenge!**
* Find a webpage of interest to your studies and use Beautiful Soup to extract the text
* Tokenise the text
* Find the most common words in your text (Extension: remove the stop words)
* Find trigrams in your text 
* Save your text to a text file

*Hint*: feel free to collude with your neighbours and please copy and paste our previous code! Copying and pasting are essential skills of developers, as well as googling error messages (seriously!). If you don't believe me, ask a computer scientist. 


```python

```
