# QUERY PDFs WITH LANGCHAIN & OPENAI

## OBJECTIVE:
- Explore options information retrival from text-based documents
- Status: SUCCESS!
    - the LANGCHAIN and OPENAI's GPT model was able to answer correctly a wide number of questions from the document
    - it can be used to automate summarization of standardized documents
        - dates, names, entities, key topics, sentiments, summarizations,...
        - possibly, we can make assesement if a set of documents provide support or not for some case of interest
        
## BASED ON:
1.) https://www.udemy.com/course/langchain-guide-next-gen-chatgpt-llms-apps-with-langchain/learn/lecture/38797056#overview

2.) https://towardsdatascience.com/4-ways-of-question-answering-in-langchain-188c6707cc5a

## TESTS:
1.) LLM's HALLUCINATION... provide question without the input document... and you still get an answer!?!??!

2.) VECTOR SEARCH
- document needs to be EMBEDED and put into a VECTOR DATABASE (ElasticVectorSearch, Pinecone, Weaviate, FAISS)
- this allows to perform similarity search between embeddings of the docuemnt and that of the query.
- test shows ability of the GPT model to answer a wide range of questions
- it returns "no information available" if question asks about element not present in the document
- we can also ask model to SUMMARIZE and asses SENTIMENT of the document with the PROMPT!!!

3.) CHAIN-TYPES
- key issue: base approach works with all data which can breach the input-rate-limits (1000-characters). 
    - thus you need to batch the input text into smaller chunks manually or use chain-types that do it automatically
- available chain types: "staff", "map_reduce", "refine", "map-rerank"
    - "staff" by default uses the whole document; all other chunk the data automatically
        - detailes of each chain-type are BELOW
- map_reduce seems to be the stronges possibly because it does use the whole information directly... although in chunks
    - other approaches respondend not only with names of the authors of the paper but also with authors found in CITATIONS!?!!?
    
4.) RetrievalQA
- A way to address the issue of working with ALL data. 
- it does initial seach for the most relevant chunks of the data!!! 
- and only those chunks are sent to OpenAI!!!
- provided correct answer
- two parameters that control the quality of answers
    - search_type="mmr", "similarity"
    - search_kwargs={"k":2} # controls number of text segments to be exteacted and sent to OpenAI
        - "similarity" required K=5 to produce consistently the correct answer
        - "mmr" required K=2!!! - cheaper and faster to run!!!
    
5.) VectorstoreIndexCreator
- wrapper on the above (4)
- requires specific data loader which i had issues to install on my comp.
- TBC...

6.) ConversationalRetrievalChain
- Like RetrievalQA, but allows to provide in the query the history of the discussion
- it was able to distribuish between the author of the paper and the authors listed in CITATIONS!!!
- Unfortunatelly, the example data does not provide interesting test case thus:
- TBC...
