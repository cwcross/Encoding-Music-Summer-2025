To see HTML rendered notebooks with dropdown code menus, go to [https://cwcross.github.io/Encoding-Music-Summer-2025/](https://cwcross.github.io/Encoding-Music-Summer-2025/). 

# Project Developement Archive

See all projects here (including PDF/MEI files and chroma databases): [https://github.com/cwcross/Encoding-Music-Summer-2025/](https://github.com/cwcross/Encoding-Music-Summer-2025/tree/main)

See rendered notebooks here: [https://cwcross.github.io/Encoding-Music-Summer-2025/](https://cwcross.github.io/Encoding-Music-Summer-2025/)  

## Github Tutorials

**Goals:**

* Edit preexisting tutorials  
  * Filter and groupby  
  * Networks and graphs  
  * Tidy data  
* Create new tutorials  
  * Mermaid Markdown  
  * RAG  
  * Structured output  
  * XML / MEI with langchain: Tool calling

**Accomplishments:**

* Made all the edits to preexisting files  
* Created and edited mermaid  
* Created and edited RAG

**Setbacks:**

* Google docs messes up formatting  
* It was initially difficult to wrap my ahead around the fact that code and outputs were embedded in the markdown file as text

**Tips:**

* Use VSCode\!\!  
* For your own code, you can create a Jupyter Notebook on the online server (with markdown cells), then can export it as markdown, then open in VSCode to make edits. It gets most of it right.  
* Use can use \<details\>\<summary\>Dropdown Title\</summary\>dropdown content…\</details\> for dropdown menus  
* You can use \`\`\`python \\n code\`\`\` for python code  
* You can use \`word\` to add a code snippet mid-sentence.


## Retrieval Augmented Generation

**Goals:**

* Create a Retrieval Augmented Generation system for:  
  * A sample of Haverford concert programs  
  * All Haverford Concert programs  
  * Vaudeville  (seperate)

**Accomplishments:**

* Created RAG apps  
* All concert programs: implemented metadata filters  
* Vauville: implemented self-check for document relevance

**Setbacks:**

* Still searching for the perfect file reader:  
  * PyPDF fails to read some docs, even with highlightable text  
  * PDFPlumber fails when there are multiple columns \- it reads across the break  
  * Neither use OCR under the hood  
* Don’t run the code that adds to the vector store more than once. It reestablishes from the persistent directory. If you run it again, you’ll create duplicates and have to start over.   
* Filters or self-checks may be needed for more complicated / very large datasets. Increase the number of samples and the chat model as needed \- a RAG is relatively cheap once the embedding is done. 

**Tips / Links:**

* Start here (understanding vector store): [https://python.langchain.com/docs/integrations/vectorstores/chroma/](https://python.langchain.com/docs/integrations/vectorstores/chroma/)   
* RAG Tutorial for our course: [https://github.com/RichardFreedman/Encoding\_Music/blob/dev\_charlie/01\_Tutorials/17\_Retrieval\_Augmented\_Generation.md](https://github.com/RichardFreedman/Encoding_Music/blob/dev_charlie/01_Tutorials/17_Retrieval_Augmented_Generation.md)  
* Langchain RAG step-by-step tutorial: [https://python.langchain.com/docs/tutorials/rag/](https://python.langchain.com/docs/tutorials/rag/)   
  * You don’t have to use Langsmith as it suggests  
* Our Vaudeville RAG code \+ our files \+ persistent directory preloaded: [https://drive.google.com/file/d/1-jnd6rZdqLY9M4lUKB3GIKaoKXW7S7mT/view?usp=sharing](https://drive.google.com/file/d/1-jnd6rZdqLY9M4lUKB3GIKaoKXW7S7mT/view?usp=sharing)   
  * Run code cell below the header “Fixes”, then see example question for template. You could turn those print statements into a function that only passes a question if you wanted to save yourself some hassle.     
  * I tried to add comments throughout to explain the steps. It’s worth looking at langchain’s RAG tutorial or similar to get a general idea of what is going on before delving too deep into the syntax for this specific app.  
* Our Haverford Concert Programs RAG \+ files for reference \+ persistent directory: [https://drive.google.com/file/d/1jyVJN8SHMeCwdFkxRdwjXu9tLTeJexSi/view?usp=sharing](https://drive.google.com/file/d/1jyVJN8SHMeCwdFkxRdwjXu9tLTeJexSi/view?usp=sharing)   
  * There’s a little more documentation about my process in this one, but a little less in terms of mid-code comments.   
  * To get this working easily, run the large code cell below the “Setting Up Filters” header. Then, you can see the question format (both including filters).  
    * Note the weird formatting for multiple filters, using `$and`. Passing two k,v pairs doesn’t work, so you have to use this weird formatting, so that it technically counts as one k,v pair. Coming to this realization was a hassle, so I figure it’s worth mentioning.  
* See the full potential of LangGraph: [https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph\_self\_rag/](https://langchain-ai.github.io/langgraph/tutorials/rag/langgraph_self_rag/)   
  * This is excessive and does not need to be fully implemented. However, one or two of the steps can be implemented. In the final version of our Vaudeville RAG, we have an llm check which documents are relevant before passing them to the chat model, but that’s all. 

## Structured Output

**Goals:**

* Create a structured output model for Vaudeville musical moments

**Accomplishments:**

* Completed the app, hosted it with streamlit, and shared with Vaudeville project for modification

**Setbacks:**

* There isn’t a ton of documentation on how to do this. You have to set a lot of it up yourself.  
* Passing too much in at once will ruin the accuracy. Find some way to chunk your documents up. We used a gpt-4o-mini call to find the exact wording of every scene header, then regex split it. 

**Tips / Links:**

* Use a Pydantic basemodel to define the output. The descriptions for each attribute are very important \- they need to tell the llm what to look for and where to find it. The basemodel class should have its own high level description too.  
*  Vaudeville Structured Output Code: [https://github.com/cwcross/vaudeville\_structured\_output/blob/main/streamlit\_app.py](https://github.com/cwcross/vaudeville_structured_output/blob/main/streamlit_app.py)   
  * With this app, you can upload an entire Vaudeville play to this and it’ll return a spreadsheet of every musical moment with relatively high accuracy for most parameters.   
* Langchain Structured output:   
  * [https://js.langchain.com/docs/concepts/structured\_outputs/](https://js.langchain.com/docs/concepts/structured_outputs/)   
  * [https://python.langchain.com/docs/how\_to/structured\_output/](https://python.langchain.com/docs/how_to/structured_output/)   
  * These give a good sense of how to bind an llm to structured output. Does not give a great sense of how to build a full app.

## Music Analysis

**Goals:**

* Evaluate the effectiveness of Large Language Models with music analysis (MEI, JSON, MusicXML)  
* Create a set of basic Music21 tools for the llm to call in its process 

**Accomplishments:**

* Created several Music21 tools that the llm could effectively access and interpret results from  
* Created a test suite of queries. For each:  
  * LLM with tools  
  * LLM without tools  
  * Ground truth

**Setbacks:**

* When feeding an LLM a dictionary, or even just an xml filepath, it cannot figure out what to feed to a tool. Rather, you have to instruct it to feed the entire prompt to each tool, including the question, and then have a helper function to parse through the response and create the datatype submitted to it as context (or find the filepaths to run Music21). This was a bit of a hurdle to figure out, but is not too difficult to work around.

**Tips / Links:**

* For the LLM without tools, passing in the full XML is often too many characters. Thus, you can convert it to a dictionary or JSON file. This loses a bit of information, but drastically reduces the character count.   
