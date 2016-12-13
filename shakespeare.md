# The Shakespeare Corpus: building classifiers

> A Naive Bayes classifier for Shakespeare’s second-person pronoun \(Mahowald 2012\)

Mahowald's research sits between historical English, computer science, psycho-linguistics and brain and cognitive sciences.

His 2012 study investigates the way that _y-_ and _th-_ pronouns alternate in the full corpus of 37 Shakespearean plays.

**==&gt; INSERT: Table 1 Pronouns used by classifier**

Mahoward uses NLTK to write a '[Naive Bayes](https://en.wikipedia.org/wiki/Naive_Bayes_classifier)' classifer. This statistical formula for probability considers each occurrence of a second-person pronoun as a 'black box' to be resolved into a _y-_ or _th-_ pronoun depending on the surrounding words. The ability  to  discriminate  between  forms  based  only  on  context is a form of collocational analysis, which we will dabble with in the activity ahead. In the case of this study, collocational analysis confirms the hypothesis that the second-person pronouns are used distinctly in the Shakespearean corpus.

Significantly,  the  words  most  useful  in  classifying  a  pronoun  as  _y-_ pronouns include high-register words such as lordship, madam, lords, and sir. After a group of conjugated second-person verbs, like 'didst' and 'hast', the words most associated with _th-_ pronouns are  words such as cursed, hateful,  and villain.

**==&gt; INSERT: Table 4 Most informative features by pronoun type**

If you have any French, you will be interested to know that these pronouns are used similarly to _Tu_ and _Vous_. _Y-_ for formal situations or when an inferior is addressing a 'social better' and _th-_ when addressing a servant, peer or other familiar persons.

