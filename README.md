# Syntactic Parser: Part-of-Sentence tagging

---

<img width="1001" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/740201eb-a16e-45ac-9832-3be097e4d801">




## Motivation

What is syntax, why does it matter, and why should we automate it?

Far from being just a theoretical exercise, syntax is essential for language processing and interpretation.
Syntax refers to the rules and principles that dictate how words and phrases are arranged to form meaningful and grammatically correct sentences. It is crucial for clarity, understanding, and effective communication, as it ensures sentences are comprehensible and convey thoughts accurately. Syntax standardises sentence construction, which is essential for consistent and clear communication.

Syntax is intimately linked to morphology (the study of word forms and structures). Morphology provides the building blocks that syntax arranges into sentences. Understanding syntax is fundamental for language learners, as it helps them form correct sentences and enhances their communication skills. Syntax also aids in disambiguation by clarifying sentence structure according to established rules.

Automating syntax checks offers several advantages. It enhances efficiency by saving time in proofreading and editing, ensuring consistency by uniformly applying syntactic rules, and is especially beneficial in professional and academic writing. In natural language processing (NLP) and computational linguistics, automated syntax analysis enables computers to understand, interpret, and generate human language, facilitating applications like machine translation and chatbots.

Case in point, when chatbots communicate with us, it is crucial that they produce sentences in a logical sequence, adhering to the word order dictated by syntax. English, like many European languages, typically follows the Subject-Verb-Object (SVO) order. Apart from stylistic and literary exceptions, any deviations from this structure would lead to rather surprising headlines. There is a saying in journalism about what makes something newsworthy: "Dog bites man, who cares? Man bites dog, now that's news!"

<img width="571" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/c9c37998-5c0f-426d-bd4b-5fe017797b3b">




This humorous maxim, grounded in a reversal of subject and object, raises an even deeper question. Without word order, without clear syntax, how else would you determine who is the perpetrator of the action and who is on the receiving end?


## Theoretical considerations 
In this repository, I am attempting to build a syntactic parser in line with dependency grammar methodology as taught in the Latin space, specifically known as *analisi logica* in Italian (see the book *Analisi logica* by Raffaella Riboni). In a nutshell, dependency grammar deals with the relationships or subordination between parts of speech (which become parts of sentence) in a sentence. It assigns labels to elements based on their function within the sentence (function to label). The three most well-known parts of a sentence are:


**Subject**: The subject of a sentence is the person, place, thing, or idea that is performing the action or being described. It is typically a noun or pronoun and is often positioned before the verb.

**Predicate (Verb)**: The predicate of a sentence tells what the subject does or is. It includes the verb and any objects, complements, or modifiers that complete the thought. The verb is the main part of the predicate, indicating the action or state of being.

**Object**: The object of a sentence is the noun, noun phrase, or pronoun that receives the action of the verb. There are two main types of objects:
- **Direct Object**: Receives the action of the verb directly. It answers the question *what?* or *whom?* after the verb.
- **Indirect Object**: Indicates to whom or for whom the action of the verb is performed. It answers the question *to whom?* or *for whom?* after the verb.


However, *analisi logica*, unlike its Anglo-Saxon counterpart, assigns much more detailed labels to words in a sentence, which constitutes the main challenge in refining the existing SpaCy modules. As a general example, English dependency syntax subsumes all prepositional objects under one umbrella term, whereas Italian makes clear distinctions between them.

<img width="1178" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/98fbd07f-dd53-4dba-b19c-5003140d46e5">








                                        Figure 1. Some prepositional objects in English


In Italian, things are much more nuanced.




<img width="1784" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/ff0e166d-0daa-4689-8959-16dbcff581e4">






                                        Figure 2. Some prepositional objects in Italian.

Italian syntax is much richer in *complementi* (objects) than other languages, as it discerns between all its prepositional objects. In other words, different prepositions mean different labels.

However, we will neglect Italian for now and instead consider Spanish, whose syntax is by no means less detailed (though the basics of it are easier to code, in my opinion). *Sintaxis tradicional* is the equivalent field of study. Building upon POS tagging, I will essentially be creating a part-of-sentence tagging module and coding the basic elements of Spanish syntax as taught in school: sujeto, predicado, complemento directo, complemento indirecto, atributo, complemento predicativo, complemento de agente, etc. I will begin with a rule-based syntactic parser but likely transition to a machine learning-powered one later on. Conceptually, part-of-sentence tagging can be implemented based on POS tagging, as parts of sentences are closely linked to parts of speech. In some cases, SpaCy already outputs parts of sentences, such as nsuj for nominative subject. However, the correlation between parts of speech and parts of sentences is not always straightforward, as the Spanish SpaCy module does not distinguish different types of objects (complementos) and only outputs 'obj' labels.






<img width="1501" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/97e93505-e969-4228-96a4-1638e61f9b70">






                                    Figure 3. Syntactic parsing diagram (translated: I gave him a gift).





This task is deceptively challenging. The way humans naturally acquire language is miraculous, and programming AI to mimic this process is even more so. While we internalise grammar rules intuitively (more often than not), machines employ 'synthetic' methods, whether rule-based or statistical, that in the end give us a glimpse into how we ourselves acquire and process language. To conclude this section with a cliffhanger, I leave the reader with the following exercise (a 'reverse syntax' exercise: going from label to function) to illustrate the practical relevance of this theoretical discussion:


**French: the many shades of the past participle**


1. J'ai *vu* une femme qui dansait.  
   Translation: I saw a woman who was dancing.

2. La femme que j'ai *vue* dansait.  
   Translation: The woman whom I saw was dancing.

Or:

3. J'ai *vu* des hommes qui dansaient.  
   Translation: I saw men who were dancing.

4. Les hommes que j'ai *vus* dansaient.  
   Translation: The men whom I saw were dancing.




Question: What causes the French verb *voir* to change like this? **🤔**

Note: *voir* past participle: vu, vue, vus, vues
Note: All French verbs behave similarly in sentences like these; it is not exclusive to this verb alone.

---
## Strategy of Implementation



### Features
- **POS Tagging**: Identifies the part of speech for each token in the input text.
- **Sentence Structure Analysis**: Determines the subject, predicate, direct object, and indirect object of a sentence.
- **Visualization**: Uses SpaCy's `displacy` to visually represent the dependency parse of the sentence.

### Installation

Install the required modules:
```bash
pip install spacy
python -m spacy download es_core_news_sm
```


The initial task is to differentiate between direct and indirect objects (complementos directos and indirectos). To achieve this, we will need to work with SpaCy labels and redefine them, as the Spanish module categorizes all objects under the general term *obj*.





