# Report on the Conceptual Graph-based Recommendation System for PRM Issues

## Introduction:
This report aims to provide an in-depth understanding of the innovative recommendation system developed to address Public Relations Management (PRM) challenges. The system relies on the use of conceptual graphs and incorporates an online learning (OL) approach to provide customized solutions for PRM challenges. Each step of the system's development will be explained in detail, incorporating code elements from the corresponding notebook.

## Step 1: Dependency Installation
The first step of this project involves installing the necessary software dependencies to run the code. The libraries used in this project include:
Pdfplumber: This library is used to extract information from PDF files, a crucial step in retrieving relevant data related to PRM.
Autocorrect: It plays a significant role in spell-checking, thereby improving the quality of extracted text.
Stanza: Used for Natural Language Processing (NLP), it enables the identification and extraction of key concepts from raw text.
PyMuPDF: This library is used to extract specific information from PDF files, facilitating the retrieval of crucial data in the context of PRM.
Transformers: Pre-trained natural language processing models are essential for certain NLP tasks, such as text auto-completion.
Textacy: This library is used for more advanced text processing tasks, such as extracting relationships between concepts.

## Step 2: Concept Extraction
The concept extraction phase is pivotal in comprehending the content of PRM-related documents.
Leveraging the BERT (Bidirectional Encoder Representations from Transformers) model, we extract titles and descriptions from PDF documents by discerning distinct title patterns and seamlessly filling in missing components within descriptions. This not only elevates data extraction and enhances PDF documents but also enables us to predict missing description segments.

In addition, the regular expression (Regex) model employed in this section of the code serves to identify specific title patterns within text extracted from a PDF page.

## Step 3: Text Extraction from PDFs
First we load the pre-trained GPT-2 language model, specifically the "gpt2-medium" variant.
Second we fine-tunes the GPT-2 model on a custom dataset for a specified number of training epochs, adjusting batch sizes and other training parameters as needed.
The fine-tuned model is saved to a designated output directory.
The code repeats the fine-tuning process for added redundancy or for multiple fine-tuning phases if necessary.

## Step 4: Create concepts dataframe
We created our initial dataframe with 6 columns:
Risk_concepts: contains the name of the concept.
Relation_Type: contains the type of relation with another concept or process (e.g. has input, is SubClass of ...).
Definition: contains the isDefinedBy part, which refers to definition of the concept, plus the isDescribedBy part.
Clean_definition: contains the isDefinedBy part, which refers to definition of the concept.
Figure: contains the isDescribedin part, which refers to a figure.
Described_in: contains the isDescribedin part, which refers to a section.
	
## Step 5: Extract and Add Relation Type, Include the Definition
In this step, we extract the phrases "described in section" and "figure" from the text and incorporate them as relation types. We then remove these phrases from the cleaned definition.

## Step 6: Pre-processing phase
Data preprocessing is essential to clean and format concept definitions. This step involves several operations, including:

Removal of stopwords, numbers, and punctuation: The NLTK library is used to eliminate stopwords, numbers, and punctuation from the definitions. This ensures that only relevant terms are retained, enhancing the text quality.

Removal of special characters: A specialized function is employed to eliminate special characters, such as emojis, symbols, and other graphical characters. This ensures that the text contains only alphanumeric characters, which is crucial for subsequent analysis.

## Step 7: From text to KB using  REBEL
This step is about  to write a function that is able to parse the strings generated by REBEL and transform them into relation triplets. This function must take into account additional new tokens used while training the model

## Step 8: Subject-Verb-Object (SVO) Relation Extraction
L'extraction de relations The extraction of subject-verb-object (SVO) relations is a crucial step in understanding how concepts are interconnected. The SpaCy library is utilized to extract these relations from sentences. Extracted SVOs are stored in a dataframe, enabling the analysis of relationships between concepts.

## Step 8: Creation of Type and Concept Relations
In this step, the code establishes relationships between concepts using two different sources:
Type Relations: The code extracts type relations from a previously created dataframe (final_triplet_unique). These type relations describe how one concept is linked to another, enhancing the understanding of concept semantics.
Concept Relations: Extracted SVOs are used to create relationships between concepts and associated processes. Process names are extracted from SVOs and added to the final dataframe, aiding in understanding how concepts are related to actions or processes.
## Step 9: Similarity Calculation
Lastly, the code employs a pre-trained BERT model to calculate similarity between two sentences. This functionality is demonstrated in an example comparing two sentences (sentence1 and sentence2) for similarity. The BERT model encodes sentences into vectors, followed by cosine similarity calculation between these vectors. This allows for the assessment of semantic proximity between concepts or sentences.

This report has provided a detailed overview of the implementation process for the recommendation system based on conceptual graphs for PRM issues. Each step has been comprehensively explained, integrating code explanations from the notebook to ensure a thorough understanding of the system and its components.
