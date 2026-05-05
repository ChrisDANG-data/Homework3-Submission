# Week 3 Project Update: Pretraining Data & Voice Agents

## Project Description

[My project is about using LLM to translate words and expressions into English, French, and Chinese with definitions, examples, synonyms, antonyms and audio pronunciations. Also, I want to build a voice agent that can answer questions about the words and expressions. Besides, it can extract vocabularies from videos like Youtube ,from PDFs and audio files. Additionally, I want to build a TTS system that can read the definitions and examples aloud. It can also do the dictation of the saved words for users. Finally, I want to build a web interface for users to interact with the system.]

## Data Pipeline Strategy

This is an ambitious and well-scoped capstone project. As a Senior ML Engineer, I’ve designed a data pipeline strategy that balances **high-quality linguistic extraction** with the **real-time requirements** of a voice agent.

Here is the recommended pipeline strategy for your Language Learning Agent.

---

### 1. Data Sources: Where to collect from?
To build a robust vocabulary extractor and translator, you need two types of data: **Reference Data** (the "truth") and **User Input Data** (the "source").

*   **Reference Data (Linguistic Knowledge):**
    *   **Wiktionary (via dumps):** Excellent for multi-language definitions, synonyms, and etymology.
    *   **WordNet:** Great for structured relationships (hypernyms/antonyms).
    *   **Tatoeba:** A massive database of sentences and translations (perfect for your "examples" feature).
*   **User Input Data (Extraction Sources):**
    *   **YouTube:** Focus on "Comprehensible Input" channels (e.g., Easy French, TedTalks).
    *   **Academic/Literature PDFs:** Research papers or classic novels.
    *   **Audio:** Podcasts or recorded lectures in the target language.

### 2. Extraction Tools: Best-in-Class for your domain
Since you are working with English, French, and Chinese, you need tools that handle multi-byte characters (Chinese) and accents (French).

*   **For YouTube:** Use `yt-dlp` to fetch the audio stream and `faster-whisper` (Large-v3 model) for transcription. Whisper is excellent at identifying the language automatically.
*   **For PDFs:** Use **Docling** (which you mentioned). It is superior to Tesseract for language learning because it understands document structure (headers vs. body text), ensuring you don't extract "Page 4 of 20" as a vocabulary word.
*   **For Web:** **Crawl4AI** is the right choice here. Use its "markdown" output mode; LLMs process markdown much better than raw HTML for identifying context around a word.
*   **For Linguistic Enrichment:** Use an LLM (GPT-4o-mini or Claude 3.5 Haiku) to synthesize the definitions, synonyms, and antonyms into a structured JSON format.

### 3. Critical Cleaning Steps
In language learning, "dirty" data leads to "bad" learning. You must implement these:

1.  **Stop-word & Frequency Filtering:** Don't extract "the," "le," or "的." Use **spaCy** to filter for "lemmas" (base forms of words) and focus on CEFR levels (A1-C2).
2.  **Deduplication:** If a user uploads three videos on "Cooking," they shouldn't see the word "Whisk" three times. Use **MinHash** to group similar context sentences.
3.  **Sentence Alignment:** For translations, ensure the source sentence and translated sentence are aligned. Tools like **LF Aligner** or LLM-based alignment are key.
4.  **ASR Hallucination Check:** Whisper sometimes "hallucinates" text during silence. Use Voice Activity Detection (VAD) to strip silent segments before processing.

### 4. Voice Capabilities: The "How"
You should split your voice architecture into two paths: **Asynchronous (Dictation)** and **Real-time (Agent).**

*   **The Voice Agent (Pipecat):**
    *   Use **Pipecat** to manage the loop: `STT (Whisper) -> LLM (Context) -> TTS (Kokoro/Edge-TTS)`.
    *   **Pro Tip:** For Chinese/French, **Kokoro** is currently the "state-of-the-art" for open-weights speed and emotion.
*   **The Dictation System:**
    *   This doesn't need to be "real-time." You can pre-generate the audio for the user's "Saved Words" using **edge-tts** (which is free and high-quality) and cache the `.mp3` files in an S3 bucket or local folder to save compute.

### 5. Estimated Volume & Processing Time
As this is a capstone, you aren't building Google Translate, but you need a "snappy" UX.

| Task | Input Size | Tool | Est. Processing Time |
| :--- | :--- | :--- | :--- |
| **Video Transcription** | 10 min Video | faster-whisper (GPU) | ~1-2 minutes |
| **PDF Extraction** | 20 pages | Docling | ~30 seconds |
| **Vocab Enrichment** | 10 words | GPT-4o-mini | ~3-5 seconds |
| **Voice Agent Latency** | 1 sentence | Pipecat + Kokoro | < 800ms (Target) |

**Data Volume Goal:** Aim to support a "Personal Library" of ~500–1,000 saved words per user. This will result in a database of roughly 50MB (text) and 500MB (cached audio clips), which is very manageable for a web interface.

### Recommended Next Step:
Start by building a **"Single-Word Pipeline"**:
1.  Input a word.
2.  LLM generates JSON (Definition, Example, Translation).
3.  Edge-TTS generates the audio.
4.  Display on the Web UI.

Once that works, move to the "Extraction Pipeline" (YouTube/PDF). Does this sequence align with your project timeline?

## Mini Pipeline Results

- Documents collected: 5
- Documents after cleaning: 5

## Reflections

### Data Strategy
- Which data sources are most relevant for your project?

I found that Extraction Tools: Best-in-Class for my domain  are useful for my project. 
Besides, Stop-word & Frequency Filtering also useful to remove common words and low-frequency terms can help focus on important vocabulary for language learning.

- Which tools from this week will you actually use in your capstone?

 The tools of this week are all useful for my project. For example, I can use TTS (edge-tts, Kokoro) to read the definitions and examples aloud. I can also use Voice agents (Pipecat framework) to build a voice agent that can answer questions about the words and expressions. Additionally, I can use Web scraping (trafilatura, Crawl4AI) to extract vocabularies from videos like Youtube ,from PDFs and audio files. Finally, I can use OCR (Tesseract, Marker, Docling) to extract text from PDFs and images.

- What's the most challenging data quality issue you expect to face?
The most challenging data quality issue I expect to save the words I consulted into a database and make sure the data is clean and organized. This includes removing duplicates, ensuring consistent formatting, and handling any errors that may occur during the extraction process. Additionally, I need to ensure that the audio pronunciations are clear and accurate, which may require some manual review and correction. Finally, I need to make sure that the definitions and examples are relevant and useful for language learners, which may require some curation and filtering of the data.

### Pipeline Execution
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

## Tools I Plan to Use

TTS, Voice Agents, database like postgreSQL etc.

## Next Steps

I may need to build my project with RAG and vector databases, if I find that the data generated by the LLM is not sufficient for my project, especially for the Chinese part of my project.
