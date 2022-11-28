# Guest Experience Feedback Insights

## Project Objective and Motivation 
Sentosa Development Corporation (SDC) is in the business of travel and hospitality where providing  a good guest experience is critical to achieve good mindshare to entice returning visitors and  ensuring guests indirectly becoming our brand ambassadors through good reviews and feedback.  To achieve a good guest experience, it is critical to be able identify key issues and compliments from  guests through various channels. This will: 
1. Enhance Operational Efficiency by extracting customer pain areas and grievances in textual data for timely action by relevant stakeholder. 
2. Auto‐Classification of feedback into key categories for analysis, trending and monitoring.

## Project Description and Details 
### Background 
The current process of extracting insights from the various data sources is a manual and onerous 
process and it entails summarization of the textual case notes/log to harness large collection of 
unstructured text data for deriving key service insights, identify pain points timely and improve 
customer satisfaction as part of Sentosa guest insights & experience (GIE) initiative. 
 
## Desired Outcomes 
### Develop MVP models for: 
- Auto summarization of the case notes/feedback logs from various channels 
- Auto categorization of feedback data received 
- Monitoring and highlight potential emerging issues and trends 
 
### Develop Visualization for: 
- Understanding of key service trends including sentiment, trending keywords, positive/negative keywords over time

## Project Deliverables 
1. Model Construct and source codes where applicable with documentation for Text Summarization Module 
2. Model Construct and source codes where applicable with documentation for Category Classification 
3. Dashboard design and construct and source codes where applicable

## My Contributions
- Webscraped travel review sites such as Klook, Tripadvisor, Traveloka and Google Reviews using Data Miner and Webscraper
- Used Part-of-Speech tag from Stanford NLP to extract combinations of bigrams and trigrams with self-written defined functions in Python code which serves as a summarisation model
- Identified the trending keywords used to describe about the attractions in Sentosa
- Classified the trending keywords according to sentiments by using Google Cloud Natural Language API for Sentiment Analysis
- Built an interactive dashboard using Tableau Desktop as deployment: https://public.tableau.com/app/profile/odelia.tan/viz/attractions_master_pos_v3_extract/Presentation

### Using Part of Speech to Extract Meaningful Keywords
#### Background
Part of speech indicates how the word functions in meaning as well as grammatically within the sentence. In English, as in many other languages, a single word can function as more than one part of speech when used in different circumstances. Understanding part of speech is essential for determining the correct definition of a word when using the dictionary. There are eight Parts of speech in the English language: noun, pronoun, verb, adjective, adverb, preposition, conjunction, and interjection.

1.	Noun  
   A noun is the name of a person, place, thing or idea. Nouns are often used with an article (the, a, an) but not always. Proper nouns always start with a capital letter; common nouns do not. Nouns can function in different roles within a sentence. For example, a noun can be a subject, direct object, indirect object, subject complement, or object of a preposition.  

      *The young **girl** asked her **mother** to bring her to the **beach** at **Sentosa** for a **picnic** and then she quickly hid under the **blanket**. Wow!*

2.	Pronoun  
   A pronoun is a word that is used in place of a noun. A pronoun is usually substituted for a specific noun, which is called its antecedent. In the italics sentence below, the antecedent for the pronoun her is the girl. Pronouns are further defined by type: personal pronouns refer to specific persons or things; possessive pronouns indicate ownership; reflexive pronouns are used to emphasize another noun or pronoun; relative pronouns introduce a subordinate clause; and demonstrative pronouns identify, point to, or refer to nouns.

      *The young girl asked **her** mother to bring **her** to the beach at Sentosa for a picnic and then **she** quickly hid under the blanket. Wow!*

3.	Verb  
   The verb in a sentence expresses action or being. There is a main verb and sometimes one or more helping verbs. (“She can dance.” Dance is the main verb; can is the helping verb.) A verb must agree with its subject number (both are singular or both are plural). Verbs also take different forms to express tense.

      *The young girl **asked** her mother to **bring** her to the beach at Sentosa for a picnic and then she quickly **hid** under the blanket. Wow!*

4.	Adjective  
   An adjective is a word used to modify or describe a noun or a pronoun. It usually answers the question of which one, what kind, or how many. (Articles [a, an, the] are usually classified as adjectives.)

      *The **young** girl asked her mother to bring her to the beach at Sentosa for a picnic and then she quickly hid under the blanket. Wow!*

5.	Adverb  
   An adverb describes or modifies a verb, an adjective, or another adverb. It usually answers the questions of when, where, how, why, under what conditions, or to what degree. Adverbs often end in -ly.

      *The young girl asked her mother to bring her to the beach at Sentosa for a picnic and then she **quickly** hid under the blanket. Wow!*

6.	Preposition  
   A preposition is a word placed before a noun or pronoun to form a phrase modifying another word in the sentence.

      *The young girl asked her mother to bring her to the beach at Sentosa for a picnic and then she quickly hid **under** the blanket. Wow!*

7.	Conjunction  
   A conjunction joins words, phrases, or clauses and indicates the relationship between the elements joined. Coordinating conjunctions connect grammatically equal elements: and, but, or, nor, for, so, yet. Subordinating conjunctions connect clauses that are not equal: because, although, while, since, etc.

      *The young girl asked her mother to bring her to the beach at Sentosa for a picnic **and** then she quickly hid under the blanket. Wow!*

8.	Interjection  
   An interjection is a word used to express emotion.

      *The young girl asked her mother to bring her to the beach at Sentosa for a picnic and then she quickly hid under the blanket. **Wow**!*

#### Methodology and Design
Native speakers possess an intuitive knowledge of parts of speech (often without an awareness of the underlying technicalities) but computers have to first understand these constituent parts of speech before they can effectively analyse language.
Part-of-speech tagging for Indonesian language has been limited and industrial-strength libraries such as Natural Language Toolkit and spaCy also do not have support for it.
For this project, Stanza, a Python natural language analysis package created by StanfordNLP, has been chosen to do Part-of-speech tagging. The toolkit is designed to be parallel among more than 70 languages, using the Universal Dependencies formalism. For each word in a sentence, Stanza assigns it a POS, and analyses its universal morphological features (UFeats, e.g., singular/plural, 1st/2nd/3rd person, etc.). To predict POS and UFeats, it adopts a bidirectional long short-term memory network (Bi-LSTM) as the basic architecture. For consistency among universal POS (UPOS), treebank-specific POS (XPOS), and UFeats, it adopts the biaffine scoring mechanism from Dozat and Manning (2017) to condition XPOS and UFeats prediction on that of UPOS.
The 17 Universal Part of Speech tags are shown in the table below.

<img src="https://user-images.githubusercontent.com/101394672/204143659-7459a316-2978-407f-9d31-7152c39a869f.png" width="600">

Using Stanza, adjectives were first chosen to be extracted as they are descriptive words that can show us what people are describing about Sentosa. Adverbs were then added as they could help to show to what extent of the descriptive words that were used. Lastly, nouns were added to help identify what was being described.
Using the concept of ngrams, a bigram would consist of an adverb and an adjective while a trigram would consist of a noun, an adverb and an adjective or an adverb, an adjective and a noun in the sequences as mentioned. The tables below show a comparison of unigrams versus bigrams vs trigrams.  

<img src="https://user-images.githubusercontent.com/101394672/204143695-7ed78a3a-f541-40b1-8835-44c68b08ac89.png" width="600">
<img src="https://user-images.githubusercontent.com/101394672/204143704-183f8435-62ef-4810-8a9d-ec92ea012516.png" width="600">
<img src="https://user-images.githubusercontent.com/101394672/204143732-97f0d21f-fa25-4c1a-a86f-3b6af949319c.png" width="600">

It can be seen that after adding adverbs and nouns to the initial unigram which was only an adjective by itself, the phrases add more meaning and context to the adjectives. Thus, for the purpose of this project, bigrams and trigrams which consisted of adverbs, adjectives and nouns were chosen to be extracted from the text corpus of reviews. For simplicity, the term ‘ngrams’ will be used to represent bigrams and trigrams throughout this chapter.
The ngrams would be run on Google Cloud Natural Language API for Sentiment Analysis which would classify them into positive, negative or neutral. This would help to group the ngrams which belong to the same sentiment together for a cleaner analysis.
Using the review ids which were uniquely tagged to all the reviews, the ngrams can be linked back to the reviews to get a bigger picture of what the Indonesians are saying about Sentosa.
All ngrams and reviews in Indonesian Language would be translated into English Language using Google Translate.

#### Findings
Using Tableau Desktop, horizontal bar charts of the frequency of positive and negative ngrams were plotted for years 2017 to 2022 for the attractions: Adventure Cove, Beach Waterfront, Cable Car, S.E.A Aquarium, Skyline Luge, Universal Studios Singapore and Wings of Time.
The image below shows the positive ngrams sorted by highest frequency for Skyline Luge in 2019.

<img src="https://user-images.githubusercontent.com/101394672/204143763-b4df1e4c-8d1d-46d3-94a7-938a664b8520.png" width="600">
<img src="https://user-images.githubusercontent.com/101394672/204143770-42e04dad-876f-415c-b836-807a2211904c.png" width="600">
<img src="https://user-images.githubusercontent.com/101394672/204143775-1172cf89-4472-4364-87e6-351309593860.png" width="600">

![image](https://user-images.githubusercontent.com/101394672/204144010-39f2b338-0941-4bbf-83d4-5a206c2bde25.png)
<sub>Sample Review for Ngram ‘better’ for Skyline Luge in 2019</sub>

![image](https://user-images.githubusercontent.com/101394672/204144029-6fd7a483-d971-4381-aa76-c8afc34cf1b7.png)
<sub>Sample Review for Ngram ‘quite satisfied’ for Skyline Luge in 2019</sub>

![image](https://user-images.githubusercontent.com/101394672/204144045-67452614-52f2-4cd9-94e5-51b6d072f196.png)
<sub>Sample Review for Ngram ‘even addicted’ for Skyline Luge in 2019</sub>

The image below shows the negative ngrams sorted by highest frequency for Skyline Luge in 2019.
<img src="https://user-images.githubusercontent.com/101394672/204144069-4dc26e61-402d-4b9f-b685-e53659af398b.png" width="600">
<img src="https://user-images.githubusercontent.com/101394672/204144076-156c552f-33b6-4655-b53b-4c7897070955.png" width="600">

![image](https://user-images.githubusercontent.com/101394672/204144089-c1850146-58cc-4bd0-8625-5221d0a2ccbb.png)
<sub>Sample Review for Ngram ‘too expensive’ for Skyline Luge in 2019</sub>

![image](https://user-images.githubusercontent.com/101394672/204144116-c9412d95-64bb-416d-aef8-b04b6d592c45.png)  
<sub>Sample Review for Ngram ‘too clear’ for Skyline Luge in 2019</sub>

![image](https://user-images.githubusercontent.com/101394672/204144130-b6694cb3-6be1-43c2-aee4-0f3722ab9308.png)  
<sub>Sample Review for Ngram ‘very complicated’ for Skyline Luge in 2019</sub>

#### Evaluation and Analysis
This model serves to narrow down the reviews to the bare minimum of the adjectives, adverbs and nouns which describes what the Indonesians are talking about for the various attractions in Sentosa.
Even though the frequency of the ngrams may be small for some ngrams, these ngrams actually serve as keywords which we can scan through to get a quick overview of what keywords Indonesians are using to describe the attractions in Sentosa. Also, these ngrams could also lead us to reviews which are of better quality and of use to Sentosa Development Corporation. Using Tableau Desktop, the dashboard allows users to interact with it by choosing whing year or attraction. One of the highlights of the dashboard is that by hovering the horizontal bar charts, users can also see the reviews which contains the ngram in both Indonesian and English Language (translated).

The image below shows the final dashboard created using Tableau Desktop.
![image](https://user-images.githubusercontent.com/101394672/204144156-ba1510ce-2123-4950-827b-acdca8721bf0.png)
![image](https://user-images.githubusercontent.com/101394672/204144165-1fe57abf-d226-4973-8920-0318d84e8d2c.png)

Overall, this model which uses part of speech to tag the reviews and extract the adjectives, adverbs and nouns out as bigrams and trigrams shows how different part of speech can be made used of to extract specific information that we want from a text corpus. This saves time and filters out unnecessary texts which users could spend long hours reading.

#### Conclusion
In this chapter, we utilised part-of-speech tagging to extract adjectives, adverbs and nouns as bigrams and trigrams to acquire meaningful keywords. These meaningful keywords, grouped by sentiments using Google Cloud Natural Language API give us insights into what Indonesians are talking about the various attractions in Sentosa in a more concise manner compared to reading the reviews individually.
