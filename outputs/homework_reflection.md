
## Notebook 01: Environment Setup

**Completed:** 2026-05-03 16:17:47

### Path Selection

- Why did you choose Path A/B/C/D?
  I chose Path D because I wanted to explore the flexibility of using both cloud APIs and google gemini.
   This allows me to compare the performance and cost-effectiveness of both approaches, 
   and to have a backup option in case one service experiences downtime.

- What trade-offs did you consider (cost vs. speed vs. flexibility)?
    I considered the trade-offs between cost, speed, and flexibility. 
    Path D offers the cost benefit and flexibility, allowing me to choose the best tool for each task. 
    However, it may also be more expensive and potentially slower than sticking to a single provider. 
    I am willing to accept these trade-offs in order to gain insights into the strengths and weaknesses of both approaches.


- Have you used Ollama before? If so, how does it compare to cloud APIs?
    I have used Ollama before and found it to be a powerful tool for local LLM deployment. 
    It offers low latency and cost savings compared to cloud APIs, but may require more setup and maintenance. 
    Cloud APIs, on the other hand, provide scalability and ease of use, but can be more expensive and have higher latency. 
    Overall, I see Ollama as a great option for certain use cases, while cloud APIs are better suited for others.

---

## Notebook 02: Web Scraping & Text Extraction

**Completed:** 2026-05-04 12:17:04

### Part 1 - trafilatura Extraction

- What URL did you choose and why?
https://github.com/openai/whisper
Because in my project, I want to use the whisper model to transcribe audio, 
so i want to see how to use Whisper and what are the features of it. 
I also want to see how well trafilatura can extract the content from a github page, which is different from a typical blog post or news article.

- How well did trafilatura extract the main content?
Trafilatura did a decent job extracting the main content from the GitHub page. 
It was able to pull out the README content, which includes the description of the project, installation instructions

- Were there any missing or incorrect parts in the extraction?
The extraction was mostly accurate, but there were some formatting issues.

---

### Part 2 - Crawl4AI vs trafilatura

- Which extractor produced better output for your test URLs?
    Crawl4AI produced better output for the test URLs, especially for the arXiv page.
    It preserved the structure and formatting of the content, which is important for LLM pretraining datasets. 
    Trafilatura did a decent job extracting the main content, but it lost some of the formatting and structure,
     which could be valuable for certain applications.   

- For what types of pages would you prefer Crawl4AI over trafilatura?
    I would prefer Crawl4AI for pages where the structure and formatting are important, such as documentation pages, technical blogs, or any content where headings, lists, code blocks, and other markdown features add value. 
    For simpler pages or when I only need the raw text without formatting, trafilatura might be sufficient.         
- How does output format (plain text vs Markdown) affect downstream LLM usage?

    The output format can significantly affect downstream LLM usage. 
    Plain text is simpler and may be easier to process for some applications, but it loses the structural information that can be crucial for understanding the content. 
    Markdown preserves this structure, which can help the LLM better understand the relationships between different parts of the text, such as which sections are headings, which are lists, and where code blocks are. 
    This can lead to better performance in tasks that require understanding of the document structure, such as question answering or summarization.

---

### Part 3 - arXiv Paper Dataset

- What topic did you choose and why?
    I chose the topic of "translation" because my project is focused on building a translation system, 
    and I wanted to see what the latest research trends are in this area.
- Were you surprised by any of the papers found?
    I was surprised to see the mojority of the papers are about NLP--using large language models for translation,
     which shows that this is a very active area of research.
- How could this scraping approach scale to build a real pretraining dataset?
    This scraping approach could be scaled to build a real pretraining dataset by automating the scraping process across multiple topics and sources. 
    We could set up a pipeline that regularly scrapes new papers from arXiv and other repositories, extracts the relevant content, and formats it for LLM pretraining. 
    Additionally, we could use more advanced scraping techniques to handle different formats and structures of academic papers, ensuring that we capture the most useful information for training our models.

---

## Notebook 03: Document OCR & PDF Extraction

**Completed:** 2026-05-04 16:15:59

### Part 1 - Tesseract OCR Quality

[TODO 1 not completed yet]

---

### Part 2 - OCR Tool Comparison

- Which tool would you choose for your capstone project's document processing needs?
 I would choose Marker for my capstone project because it offers a comprehensive PDF-to-Markdown conversion that preserves complex layouts, tables, and special formatting. This would allow me to extract high-quality text data from a wide variety of documents, which is crucial for building a robust LLM pretraining dataset. Marker’s ability to handle complex documents and its focus on Markdown output makes it ideal for preparing data that can be easily ingested by LLMs, while also maintaining the structure and context of the original
- How has OCR technology evolved from Tesseract to Marker/Docling?
 OCR technology has evolved significantly from Tesseract to modern tools like Marker and Docling. 
 Tesseract, developed in 2006, was one of the first widely available OCR engines and focused primarily on extracting text from images. 
 It works best with simple layouts and can struggle with complex documents, tables, and special formatting.
- What role does layout awareness play in extraction quality?
    Layout awareness is crucial for extraction quality, especially for documents with complex structures. 
    Tools like Marker and Docling that preserve layout can maintain the context and relationships between different elements (e.g., tables, images, code blocks),
    which is essential for creating high-quality training data for LLMs. In contrast, tools that do not preserve layout may produce disorganized text that loses important contextual information, leading to lower quality data for model training.

---

## Notebook 04: Speech Recognition (ASR)

**Completed:** 2026-05-04 18:44:30

### Part 1 - ASR in Pretraining

- How does ASR transcription quality compare to web-scraped text?
 ASR transcriptions can contain errors such as misheard words, incorrect punctuation, and lack of formatting. 
 Web-scraped text is typically cleaner but may still have issues like HTML artifacts or OCR errors.

- Which model size would you choose for transcribing 1000 hours of podcasts?
 I would likely choose the "small" model for a balance of speed and accuracy. 
 The "tiny" model may be too inaccurate, while the "base" model may be too slow for large volumes.

- What are the ethical considerations of transcribing public audio content?
Well, there are several ethical considerations to keep in mind when transcribing public audio content:
1. **Privacy**: Even if the audio is publicly available, it may contain sensitive information about individuals. Transcribing and using this data without consent can lead to privacy violations.
2. **Copyright**: Many audio sources, such as podcasts and YouTube videos, are
protected by copyright. Transcribing and using this content for training without permission may infringe on intellectual property rights.
3. **Bias**: ASR models may have biases that affect transcription quality for certain accents
or dialects. This can lead to underrepresentation of certain groups in the training data, which may perpetuate biases in the resulting LLM.
4. **Misinformation**: If the audio content contains misinformation or harmful content,
transcribing and including it in training data can lead to the LLM learning and reproducing that misinformation.
5. **Transparency**: It's important to be transparent about the sources of training data and the
methods used for transcription, so that users of the LLM can understand the potential limitations and biases in the model.

---

### Part 2 - Custom Transcription

- What audio did you transcribe?
    I transcribed sample-1.mps in test data

- How accurate was the transcription?
   THe transcription was fairly accurate, capturing the main content of the audio. 
   However, there were some errors . 


- What would you change for better results (model size, preprocessing)?

    I would experiment with the "small" model for better accuracy, as the "tiny" model may have been too error-prone. 
    Additionally, I would consider preprocessing the audio to enhance clarity, such as noise reduction or normalization, which could improve transcription quality.

---

## Notebook 05: Data Cleaning Pipeline

**Completed:** 2026-05-04 23:54:58

### Part 1 - Pipeline Stage Analysis

- Which cleaning stage removed the most documents? Why?
The removal of HTML noise (Experiment 2a) removed the most documents. This is because several of the raw documents contained HTML tags and structures that were stripped out, leaving behind empty or very short text. For example, the document with the news article had a lot of HTML elements that were removed, resulting in a much shorter cleaned version.

- Were there any false positives (good content incorrectly removed)?
Yes, there were some instances where legitimate content was removed during the HTML noise removal process. This happened when the HTML tags were embedded within the text or when the stripping process inadvertently removed important information.


- How would you adjust the deduplication threshold for different use cases?
The deduplication threshold can be adjusted based on the desired balance between retaining similar content and removing duplicates. For use cases where diversity is important (e.g., training a generative model), a lower threshold (e.g., 0.5) might be used to remove more similar documents. For use cases where precision is key (e.g., information retrieval), a higher threshold (e.g., 0.9) might be preferred to retain more documents that are only slightly different.

---

### Part 2 - Scaling with DataTrove

- What additional cleaning steps would you add to your pipeline?
 I would consider adding a step for removing boilerplate content, such as navigation menus, footers, and advertisements, which can be common in web-scraped data. This could be done using a library like Boilerpipe or by training a custom model to identify and remove such content.

- How would you handle the scale difference between 10 documents and 10 billion?
To handle the scale difference, I would leverage distributed computing frameworks like Apache Spark or Dask to parallelize the processing across a cluster of machines. For storage, I would use a distributed file system like HDFS or cloud storage solutions that can handle large volumes of data. Additionally, I would implement efficient batching and streaming techniques to process the data in chunks rather than loading everything into memory at once.

- What was the most surprising thing you learned about DataTrove/FineWeb?
One surprising aspect of DataTrove and FineWeb is their use of advanced deduplication techniques that go beyond simple hashing. They utilize a combination of MinHash and more sophisticated similarity measures to identify near-duplicate content, which allows them to retain more unique documents while still removing redundant ones. Additionally, their ability to process and clean data at such a massive scale while maintaining high quality is impressive, showcasing the importance of efficient algorithms and infrastructure in large-scale data processing.

---

## Notebook 06: Text-to-Speech & Voice Synthesis

**Completed:** 2026-05-05 00:23:21

### Part 1 - TTS Synthesis

- How natural did the synthesized speech sound?
 I found the synthesized speech to be quite natural, with clear pronunciation and appropriate intonation. The voice I chose had a conversational tone that made it sound more engaging and less robotic compared to some other TTS systems I've heard.

- Which voice did you prefer and why?
I preferred the "en-US-AriaNeural" voice because it had a warm and friendly tone that made the synthesized speech sound more human-like. The intonation and pacing were well-suited for the content I was synthesizing, which made it easier to listen to and understand.

- What are the limitations of cloud-based TTS like edge-tts?
 Well, one limitation is that it requires an internet connection to access the cloud service, which can be a problem in areas with poor connectivity. Additionally, there may be latency issues when synthesizing longer texts, and there could be concerns about data privacy since the text is sent to a third-party service for processing. Finally, while the voices are quite good, they may still lack the full expressiveness and emotional range of human speech in certain contexts.

---

### Part 2 - Voice Agent TTS Architecture

[TODO 2 not completed yet]

---

## Notebook 07: Voice Agent with Pipecat

**Completed:** 2026-05-05 14:57:16

### Part 1 - Custom Voice Agent

- Did the agent maintain context across turns?

yes, the agent was able to maintain context across turns. 
Each response built upon the previous questions and answers, demonstrating an understanding of the ongoing conversation. The agent referenced earlier points and provided coherent answers that were relevant to the user's questions.
- What persona did you choose and how well did it work?
I chose the persona of a helpful, experienced AI engineer who explains complex concepts in simple terms. 
I think it worked well for the questions I asked, as the responses were clear, informative, and tailored to someone seeking to understand AI concepts without too much technical jargon.

- What would you change to make the conversation more natural?
Well, I might try to make the responses a bit more conversational and less formal.
Adding some casual language or examples could make it feel more like a natural dialogue rather than a textbook explanation. 
Additionally, I could experiment with adjusting the temperature parameter to allow for more creative and varied responses

---

### Part 2 - Production Architecture

- Would you use Pipecat or build your own FastAPI voice server? Why?
I would likely choose to use Pipecat for building the voice agent.
The main reasons are:
1. Development Effort: Pipecat provides a lot of built-in functionality for handling the complexities of real-time voice processing, such as WebRTC transport, VAD, and turn detection.
2. Scalability: Pipecat is designed to handle multiple concurrent voice sessions and can scale more easily than a custom-built FastAPI server.
3. Latency: Pipecat's optimizations for real-time voice processing may result in lower latency compared to a custom implementation, especially if I don't have extensive experience with real-time audio processing.
Overall, using Pipecat would allow me to focus more on the unique aspects of my voice agent rather than reinventing the wheel for common voice processing tasks.                



- What's the most challenging part of building a real-time voice agent?

The most challenging part of building a real-time voice agent is managing the latency and ensuring a seamless user experience.
This involves optimizing the ASR, LLM, and TTS components to work efficiently together while also handling network delays and processing times.
 Additionally, implementing robust error handling and managing interruptions (e.g., user speaking while the bot is still talking) can be complex, as it requires the system to

- How would you handle the case where the user interrupts the bot mid-sentence?

To handle user interruptions mid-sentence, I would implement a mechanism to detect when the user starts speaking while the bot is still talking.
 This could be achieved using Voice Activity Detection (VAD) to monitor for user input during the bot's response. If an interruption is detected,
  the system could immediately stop the TTS output and prioritize processing the new user input. The conversation context would need to be updated accordingly, 
  and the bot could respond to the new input while also acknowledging the interruption if appropriate. This approach ensures a more natural and responsive interaction, 
  allowing users to feel heard and engaged in real-time conversations.

---

## Notebook 08: Project Integration

**Completed:** 2026-05-05 16:40:11

### Data Pipeline Strategy

- Which data sources are most relevant for your project?

I found that Extraction Tools: Best-in-Class for my domain  are useful for my project. 
Besides, Stop-word & Frequency Filtering also useful to remove common words and low-frequency terms can help focus on important vocabulary for language learning.

- Which tools from this week will you actually use in your capstone?

 The tools of this week are all useful for my project. For example, I can use TTS (edge-tts, Kokoro) to read the definitions and examples aloud. I can also use Voice agents (Pipecat framework) to build a voice agent that can answer questions about the words and expressions. Additionally, I can use Web scraping (trafilatura, Crawl4AI) to extract vocabularies from videos like Youtube ,from PDFs and audio files. Finally, I can use OCR (Tesseract, Marker, Docling) to extract text from PDFs and images.

- What's the most challenging data quality issue you expect to face?
The most challenging data quality issue I expect to save the words I consulted into a database and make sure the data is clean and organized. This includes removing duplicates, ensuring consistent formatting, and handling any errors that may occur during the extraction process. Additionally, I need to ensure that the audio pronunciations are clear and accurate, which may require some manual review and correction. Finally, I need to make sure that the definitions and examples are relevant and useful for language learners, which may require some curation and filtering of the data.

---

### Mini Pipeline Results

- What data did you collect and how did you clean it?
In fact, for my project, I don't need to collect data from the web. 
Instead, I will use the LLM to generate the data I need for my project. 
For example, I can use the LLM to generate definitions, examples, synonyms, antonyms and audio pronunciations 
for the words and expressions I want to translate.
 Additionally, I can use the LLM to generate questions and answers for the voice agent that can answer questions about the words and expressions. Finally, I can use the LLM to generate text for the TTS system that can read the definitions and examples aloud.

- Were any documents removed by the pipeline? Why?
No documents were removed by the pipeline. 
However, I did use some cleaning steps to ensure that the data is clean and organized. 
For example, I removed duplicates, ensured consistent formatting, and handled any errors that may occur during the extraction process. Additionally, I made sure that the audio pronunciations are clear and accurate, which may require some manual review and correction. Finally, I made sure that the definitions and examples are relevant and useful for language learners, which may require some curation and filtering of the data.

- How would you scale this to a full dataset for your project?
I will scale this to a full dataset for my project by using the LLM to generate a large amount of data for my project.

---
