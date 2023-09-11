# Transformer Based Information Retrieval (IR) System

In this project, we prototype the IR product that will <b>recieve an input string and return the most relevant offers</b> to the user with respect to that code. It uses a <a href="https://github.com/federico2001/QueryTypeDetector">transformer model for text classification</a> to detect the type of query, then depending on the type, it applies a series of procedures to find the best match (text similarity using TF-IDF, cosine similarity, stemming and lemmatization, "fuzzy" similarity, data augmentation (through synonym generation) 

These are the steps taken to achieve this:
- Load libraries and define functions.
- Given an input text, <b>get the category</b> classified by our TypeDetector service which we consume through an API.
- Depending on the response (0 = Retail, 1 = Brand, 2 = Category) we perform a specific treatment.
- If the <b>type of query is 0 or 1</b>, we search for a match with our unique retailers or brands by performing <b>TF-IDF</b> and <b>Cosine Similarity</b>.
- Also, we compute a '<b>fuzzy similarity</b> score' in case there are typeos, which can be helpful if the cosine similarity doesn't bring relevant results.
- Next, we fetch offers that come from our matched retailers or brands, only if the cosine similarity is > 0.9 or the fuzzy similarity is > 0.75
- If the <b>type of query is 2</b>, then the similarity of the term is compared to offers directly, and synonyms of the terms are computed and also compared to the offers to contemplate a wider range of relevant results.
- Finally, the relevant offers are returned in a json list along with a log of activity.

<b>*IMPORTANT NOTE</b>: the similarity score is only returned if the type of query is 'category' as in the other cases the only match is with respect to the retailer or brand and that similarity is returned in the log.
