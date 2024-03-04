# Overview
This project presents a Named Entity Recognition (NER) model aimed at classifying words into various categories based on their context, such as person names, locations, organizations, etc. The model leverages the complexity of NLP tasks where context significantly influences the meaning and classification of words.

##Introduction
The motivation behind this NER model is to accurately identify and classify named entities in text, even when the context makes the classification challenging. The model is designed to differentiate between common words and named entities, improving the understanding and processing of natural language.

## Model Components:
1. **GloVe Word Embedding**: The model starts with a word embedding layer utilizing pre-trained GloVe embeddings from the "glove-wiki-gigaword-100" dataset, which contains a vocabulary of 40k words. This choice is strategic to leverage a vast semantic network without the computational cost of training the embedding from scratch.

2. **LSTM Layers**: The embedding layer is followed by RNN layers, specifically a bi-linear LSTM with 2 hidden layers. This configuration was found to offer the best performance, likely due to LSTM's capability to remember long-term dependencies, which is crucial for understanding context in language.

3. **Classifier Level 1**: A classifier with 3 labels (likely 'O' for non-entities, and two others for different types of entities) assists the model in recognizing named entities. This classifier includes the same GloVe embedding layer, a bi-linear LSTM, and a fully connected layer. The inclusion of this classifier significantly improves the model's performance by reducing the misclassification of named entities as non-entities ('O').

4. **PoS Tagger**: The model incorporates a pre-trained Part-of-Speech (PoS) tagger from NLTK, which provides 43 possible tags. Since most named entities are nouns (proper or common), the PoS tagger adds a layer of syntactic information that helps refine the model's predictions.

5. **Classifier Level 2**: This component consolidates the outputs from the previous layers and classifiers. It comprises the GloVe embedding, two layers of bi-linear LSTM, two fully connected layers, and an output layer. The output layer integrates the outputs from the previous fully connected layer, the PoS tagger, and the logits from classifier level 1, offering a comprehensive analysis for final entity classification.

## Dataset Insgiths

To enhance the description of the dataset used for training the NER model, consider the following refined explanation:

The dataset employed in this project is a meticulously labeled collection of approximately 39,000 words, each classified into one of 13 distinct classes following the Inside-Outside-Beginning (IOB) tagging convention. This convention is a common format in Named Entity Recognition tasks, providing a granular level of entity distinction by marking not only the presence of an entity but also its position within a multi-word entity. The classes include:

- **O**: Non-entity words, indicating that the word does not represent a named entity.
- **B-PER**, I-PER: Beginning and Inside tags for person names, identifying individuals.
- **B-LOC**, I-LOC: Location tags, marking the start and continuation of geographical entities such as cities or countries.
- **B-ORG**, I-ORG: Organization tags, used for the initial and subsequent words in the names of organizations.
- **B-MISC**, I-MISC: Tags for miscellaneous entities that don't belong to the person, location, or organization categories.
- **B-GRP**, I-GRP: Tags for groups, including bands, teams, and collectives.
- **B-CW**, I-CW: Tags for creative works, including titles of books, songs, and movies.
- **B-CORP**, I-CORP: Tags used for corporations, identifying business entities.
- **B-PROD**, I-PROD: Product tags, marking the names of specific products.
