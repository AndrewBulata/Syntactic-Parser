# Syntactic Parser

## Motivation: 
What is syntax, why does it matter, and why should we automate it?

Far from being just a theoretical exercise, syntax is essential for language processing and interpretation.
Syntax refers to the rules and principles that dictate how words and phrases are arranged to form meaningful and grammatically correct sentences. It is crucial for clarity, understanding, and effective communication, as it ensures sentences are comprehensible and convey thoughts accurately. Syntax standardises sentence construction, which is essential for consistent and clear communication.

Syntax is intimately linked to morphology (the study of word forms and structures). Morphology provides the building blocks that syntax arranges into sentences. Understanding syntax is fundamental for language learners, as it helps them form correct sentences and enhances their communication skills. Syntax also aids in disambiguation by clarifying sentence structure according to established rules.

Automating syntax checks offers several advantages. It enhances efficiency by saving time in proofreading and editing, ensuring consistency by uniformly applying syntactic rules, and is especially beneficial in professional and academic writing. In natural language processing (NLP) and computational linguistics, automated syntax analysis enables computers to understand, interpret, and generate human language, facilitating applications like machine translation and chatbots.

## Implementation 
In this repository, I am attempting to build a syntactic parser in line with dependency grammar methodology as taught in the Latin space, what is known as 'analisi logica' in Italian (see the book 'Analisi logica' by Raffaella Riboni). In a nutshell, dependency grammar deals with the relationship or subordination between parts of speech (which become parts of sentence) in a sentence. Specifically, analisi logica, unlike the anglo-saxon counterpart, assignes more detailed labels to words in a sentence, which constitutes the main challenge to refining the already existing SpaCy modules. As a general example, English dependency syntax subshumes all objects preceded by prepositions under the term 'prepositional object', whereas Italian makes a clear distinction betwen all them.

<img width="1138" alt="image" src="https://github.com/AndrewBulata/Syntactic-Parser/assets/64040990/f8dc7a30-ab3c-437b-b50d-54034eeedbfc">




