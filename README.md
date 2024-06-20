# Syntactic Parser


<img width="976" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/0d19819f-ce08-4a26-878e-49c1c87b56cb">



## Motivation: 
What is syntax, why does it matter, and why should we automate it?

Far from being just a theoretical exercise, syntax is essential for language processing and interpretation.
Syntax refers to the rules and principles that dictate how words and phrases are arranged to form meaningful and grammatically correct sentences. It is crucial for clarity, understanding, and effective communication, as it ensures sentences are comprehensible and convey thoughts accurately. Syntax standardises sentence construction, which is essential for consistent and clear communication.

Syntax is intimately linked to morphology (the study of word forms and structures). Morphology provides the building blocks that syntax arranges into sentences. Understanding syntax is fundamental for language learners, as it helps them form correct sentences and enhances their communication skills. Syntax also aids in disambiguation by clarifying sentence structure according to established rules.

Automating syntax checks offers several advantages. It enhances efficiency by saving time in proofreading and editing, ensuring consistency by uniformly applying syntactic rules, and is especially beneficial in professional and academic writing. In natural language processing (NLP) and computational linguistics, automated syntax analysis enables computers to understand, interpret, and generate human language, facilitating applications like machine translation and chatbots.

Case in point, when chatbots communicate with us, it is crucial that they produce sentences in a logical sequence, adhering to the word order dictated by syntax. English, like many European languages, typically follows the Subject-Verb-Object (SVO) order. Apart from stylistic and literary exceptions, any deviations from this structure would result in jumbled sentences. There is a saying in journalism about what makes something newsworthy: "Dog bites man, who cares? Man bites dog, now that's news."

<img width="577" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/c9d97cbe-ed90-41b6-b234-2aa784d35964">


How else would you determine who is the perpetrator of the action and who is on the receiving end without word order?

## Implementation & theoretical considerations
In this repository, I am attempting to build a syntactic parser in line with dependency grammar methodology as taught in the Latin space, specifically known as *analisi logica* in Italian (see the book *Analisi logica* by Raffaella Riboni). In a nutshell, dependency grammar deals with the relationships or subordination between parts of speech (which become parts of sentence) in a sentence. It assigns labels to elements based on their function within the sentence (function to label). Specifically, *analisi logica*, unlike its Anglo-Saxon counterpart, assigns much more detailed labels to words in a sentence, which constitutes the main challenge in refining the existing SpaCy modules. As a general example, English dependency syntax subsumes all prepositional objects under one umbrella term, whereas Italian makes clear distinctions between them.

<img width="1170" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/33ee8c2c-b096-4270-bff2-b2791c1975a5">





                                                  Figure 1. Some prepositional objects in English


In Italian, things are much more nuanced.




<img width="1784" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/ff0e166d-0daa-4689-8959-16dbcff581e4">






                                                  Figure 2. Some prepositional objects in Italian.

Italian syntax is much richer in *complementi* (objects) than other languages, as it discerns between all its prepositional objects. In other words, different prepositions mean different labels.

However, we will neglect Italian for now and instead consider Spanish, whose syntax is by no means less detailed (though the basics of it are easier to code, in my opinion). *Sintaxis tradicional* is the equivalent field of study. Building upon POS tagging, I will be coding the basic elements of Spanish syntax as taught in school: sujeto, predicado, complemento directo, complemento indirecto, atributo, complemento predicativo, complemento de agente, etc. I will start by building a rule-based syntactic parser, but I will most likely transition to a machine learning-powered one later on. 








<img width="1501" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/97e93505-e969-4228-96a4-1638e61f9b70">






                                    Figure 3. Syntactic parsing diagram (translated: I gave him a gift).





This task appears deceptively challenging. The way humans naturally acquire language is miraculous, and programming AI to mimic this process is even more so. While we internalise grammar rules intuitively (more often than not), machines employ 'synthetic' methods, whether rule-based or statistical, that in the end give us a glimpse into how we ourselves acquire and process language. To conclude this section with a cliffhanger, I leave the reader with the following exercise (a 'reverse syntax' exercise: going from label to function) to illustrate the practical relevance of this theoretical discussion:


French

1. J'ai *vu* une femme qui dansait.  
   Translation: I saw a woman who was dancing.

2. La femme que j'ai *vue* dansait.  
   Translation: The woman whom I saw was dancing.

Or:

3. J'ai *vu* des hommes qui dansaient.  
   Translation: I saw men who were dancing.

4. Les hommes que j'ai *vus* dansaient.  
   Translation: The men whom I saw were dancing.




What causes the French verb *voir* (past participle: vu, vue, vus, vues) to change like this? **🤔**








