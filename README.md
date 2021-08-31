# Introduction
*Homeric Greek* by Clyde Pharr offers an introduction to Ancient Greek learners through Homer's *Iliad*, but with a twist. He lays out the book such that students can immediately begin reading the first book of the *Iliad*, basing each chapter's grammar concepts and vocabulary words on what appears first.

This method of immediately immersing students in ancient texts, rather than walking them through artificially made sentences to demonstrate grammar concepts, makes the most sense in aiding students to get used to reading actual texts. The main drawback of this method is that ancient texts are usually very unapproachable to beginners, and therefore, they might feel discouraged from continuing. 

The question is, then, how can we make this method more approachable? What can we implement to aid students in their introduction to Ancient Greek in this way? 

This writeup consists of my explorings in creating tangible figures, sentences, and models for Ancient Greek students to reference. My goal is to provide tools for students, so that learning directly from the ancient texts feels more approachable and streamlined.

<br/>

# Querying Frequencies and Forms of Verbs

## Recalculation of Pharr's Verb Frequency Table
In the preface of *Homeric Greek*, Pharr includes an aggregate table (created by Professor Frank E. Robbins of the University of Michigan) containing frequencies for verb forms. Considering the book was published in 1918, the frequencies were done by hand and came from a small sample size.

Using the Ancient Greek Dependency Treebank (AGDT), I recreated more accurate tables of verb frequencies by authors, their works, as well as an aggregate table. To query for these figures, I used both XQuery and Python (using the ElementTree API).

> The tables comparing Pharr's figures vs my figures can be found [**here**](https://docs.google.com/spreadsheets/d/1qGaYBmSPbymfAWAhbouILWmVVnCR3vS3SwANmYWMhJM/edit?usp=sharing).

> The tables for other authors (including Homer) in the ADGT can be found [**here**](https://docs.google.com/spreadsheets/d/1QMc367YDlCfRuuwIZYOhZw4ZAEJTqoW8wsmbOngY9Eo/edit?usp=sharing). 

> The tables for Epictetus *Enchiridion* can be found [**here**](https://docs.google.com/spreadsheets/d/1imoM_K7HFY0sK-54jYRFYlT9oRI-ZcGjCSNJk7plfPE/edit?usp=sharing).

> The sorted data from the tables can be found [**here**](https://docs.google.com/spreadsheets/d/1ENGLoQzy5xFD5fQm-LTHR0DNqIOUP_2Kr5N4CzHCek0/edit?usp=sharing).

<br/>

Because the book is focused on Homeric Greek, I analyzed and compared the frequency tables I queried from the *Iliad* and the *Odyssey* with Pharr's frequency tables. The figures I was able to query for were surprisingly quite different from Pharr's tables, the most significant difference being that in my figures, the thematic aorist indicative active and the thematic imperfect indicative active were the two most common verb forms, while in Pharr's figures, these forms were placed 3rd and 4th in frequency.

The differences in the figures are likely present because Pharr's tables contained samples from Euripedes, Herodotus, Demosthenes, Xenophon, as well as Homer, and only 10 pages from each author were included in the samples. In contrast, my sample consisted only of the *Iliad* and the *Odyssey*.

These verb frequencies can be used to decide what forms are most important for students to master, in order for them to read and understand ancient texts as soon as possible. In conjunction with an implementation using this data (for example, a javascript program that highlights all verb forms that students have learned thus far in the ancient text), these updated figures could be useful for students beginning to learn Ancient Greek.

<br/>

## Querying for Verb Forms
In addition to calculating these frequencies, I used the ElementTree API to write a Python script that queries for lists of specified verb forms with details about the form, lemma, citation, etc. More specifically, the script also accounts for specialized verb forms (for example, subjunctives modified by ἄν).

> Example tables summarizing the figures and examples of verb forms can be found [**here**](https://docs.google.com/spreadsheets/d/1hXhT_BvIeOyJbt22DaBieFxKIxjUKBtLXcdct3vV1yw/edit?usp=sharing).

<br/>

# Querying for sentences from the *Iliad*

Pharr's focus on immersing students in the first book of *Iliad* as soon as they start is one way to approach introducing new students using ancient texts, but there are other supplemental ways to immerse students using real sentences from the text. In particular, I focused on following Pharr's chapter layouts (which follow the order that grammatical concepts show up in the *Iliad*) and providing additional sentences (also from the *Iliad*) that demonstrate the same concepts explained in his chapters. This way, students will be able to see multiple real sentences from different parts of the *Iliad* that act as examples to the chapter content, without relying on artificial sentences that exist solely to demonstrate grammatical conepts.

Using the AGDT, I was able to pull out sentences that corresponded to each chapter's content. These sentences are sorted from shortest to longest, since shorter sentences are more digestible when used for the purpose of viewing several examples.

> Chapters 3 - 20 can be found [**here**](https://docs.google.com/spreadsheets/d/1MfMHK5HouwF7xLAwP3jNJA4CJNeBTG-kplrKEOe6JBs/edit?usp=sharing).

> Chapters 21 and on can be found [**here**](https://docs.google.com/spreadsheets/d/1qkPu49XhlHNkY1iXMKG3_pfvm66Z-v0lmt8VMXkdzxY/edit?usp=sharing).

<br/>

# Sentence alignment for Ancient Greek and English

For new learners to Ancient Greek, a wall of text containing only Ancient Greek can seem incredibly daunting and unreadable! One way to make it more approachable is to break it up sentence by sentence and align each sentence to its English translation. With this sentence alignment, students would be able to get the gist of what is going on in the text and be able to study the sentences side by side in greater detail. 

I created a Python script (using networkx and ElementTree) that takes in Greek and finds the English alignment. Specifically, this script was used in another program that made the Cunliffe library interactive and searchable, in which it was used to align the Greek examples of each entry to the English translations. 

> The clean GitHub page of all my examples is coming soon!

<br/>

# Modeling interactive networks and trees

## Networks

Using the networkx package in Python, I was able to create interactive networks demonstrating relationships between specified word types (such as part of speech, function in sentence, etc). Cytoscape and Gephi were used to make the generated networks viewable and interactive. 

The networks had weighted directed links (the links point an arrow to the node it is modifying and scale visually based on the weight) and weighted nodes that scaled visually.

Some examples of networks I was able to generate include:
 * conjunction and object relations
 * conjunction and predicate nominative (PNOM) relations
 * conjunction and subjunctive relations
 * object to object relations
 * PNOM to PNOM relations
 * subject to subject relations
 * preposition and object relations
 * verb and subject relations
 * verb and object relations

These networks are useful for viewing how specific words interact with each other, as well as viewing this data in an easily digestible format. Students would be able to notice the similarities and differences in word relations without having advanced knowledge of Ancient Greek. For example, they might notice that certain prepositions tend to modify certain objects based on the weight of the links connecting the two words, or that certain subjects tend to do certain actions based on the links that connect the subject to verb.

One drawback of using networks to view word relationships is that there are usually too many nodes for Cytoscape and Gephi to handle easily, if each node represents a specific lemma or form. However, it can be more easily used to illustrate general relationships between categories of words, or relationships between words within a more limited sample.

> The clean GitHub page of all my examples is coming soon!

<br/>

## Trees

The AGDT is represented by sentences organized as trees (hence "Treebank"), but the raw data is difficult to interpret and understand how the words are organized and related. I worked on creating interactive visualizations of these trees using the d3.js package in Javascript. Specifically, I used the TidyTree package from d3 to create visualizations.

The visualization consists of a collapsible tree (laid out horizontally, from left to right), in which you can click nodes to collapse or expand each of their branches, so that students can focus on specific clauses and relations without visual crowding or clutter. Each node is labeled with its form, and each link is labeled with the nodes' relations. Mousing over the node creates a tooltip that provides more details about the node (such as its form, lemma, citation, relation, etc).

Some things that I had in mind for further development were:
* highlighting immediate children and parents of the selected node
* connecting node color schemes to correspond with what students have already learned vs what they have not learned, to mark what they should be able to identify
* creating a quiz-like/game-like function to the trees, in which students would be able to practice guessing what relation two nodes might have, etc.

> I'm not quite sure how to get this easily viewable in GitHub - I'm working on finding something that works without having to install packages!

More recently, I've been using Vue.js to tinker with the interactive dependency trees on the Scaife Viewer with Eldarion. The Scaife Viewer already has many of the planned and implemented aspects of the visualizations I worked on with d3, but on a much more polished level. However, one drawback is that the trees are difficult to view fully, and users need to use the scroll bar to be able to see each node and its' respective branches. I am currently working on learning how to use Vue better, so that I can help with this!

<br/>
