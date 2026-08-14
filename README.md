# 🤖 PRUHelper AI

**AI Powered Financial Information Assistant**

PRUHelper AI is an experimental AI powered financial assistant originally developed as part of **PRUClarity**, now known as **Clarity+**, during the **PolyFinTech100 API Hackathon 2025**.

The feature was designed to help users understand financial, insurance, healthcare, and policy related information by combining a document knowledge base with live web search and AI generated responses.

> **Project Status**
>
> PRUHelper AI was an experimental feature developed during the early development of PRUClarity.
>
> The feature was later **removed from the final Clarity+ product** and this repository is retained as a showcase of the original prototype and technical exploration.

## 💡 The Idea

Financial and insurance information can often be difficult to understand because relevant information is distributed across policy documents, websites, announcements, and other sources.

PRUHelper AI explored a simpler interaction:

```text
User Question
     ↓
Internal Knowledge Base
     ↓
Relevant Information Found?
     ↓
Yes → Generate Answer
No  → Search the Web
     ↓
Clean & Process Results
     ↓
AI Generated Response
```

Instead of requiring users to manually search through multiple sources, the assistant attempted to retrieve relevant information and present it in a clearer format.

## ✨ Features

* 🤖 AI powered financial assistant
* 📚 Retrieval Augmented Generation using PDF documents
* 🔎 Live Google Search fallback
* 🧠 OpenAI language model integration
* 📄 PDF knowledge base support
* 🔢 Vector based document retrieval
* 🧹 Search result cleaning and processing
* 📅 Policy date extraction
* 🏥 Insurance and healthcare focused query handling
* 📋 Structured AI generated responses
* 🔗 Source aware web search results
* 💬 Simple natural language interface
* 🎨 Streamlit based user interface

## 🧠 Hybrid Retrieval Approach

PRUHelper AI uses a hybrid information retrieval workflow.

The assistant first attempts to answer a query using its local document knowledge base.

```text
User Query
    ↓
PDF Knowledge Base
    ↓
Vector Retrieval
    ↓
Relevant Answer Found?
   / \
 Yes  No
  ↓    ↓
 RAG  Google Search
  \    /
   ↓
AI Response
```

This allows the system to prioritise curated information while still being able to search for external information when required.

## 📚 Retrieval Augmented Generation

PRUHelper AI uses **LlamaIndex** to build a retrieval augmented generation pipeline.

Documents placed within the configured document directory can be loaded into a vector index.

The system then retrieves the most relevant document content for a user's question before generating a response.

The RAG workflow includes:

```text
PDF Documents
      ↓
Document Loading
      ↓
Embeddings
      ↓
Vector Index
      ↓
Similarity Retrieval
      ↓
Relevant Context
      ↓
AI Generated Answer
```

The project uses **FastEmbed** for document embeddings.

## 🌐 Live Web Search

If the document knowledge base cannot provide sufficient information, PRUHelper AI falls back to a web search.

The search workflow:

1. Accepts the user's query.
2. Performs a Google Search.
3. Retrieves relevant search results.
4. Cleans unnecessary metadata.
5. Extracts important information.
6. Sends the processed context to the language model.
7. Generates a structured response.

This was intended to help the assistant answer questions involving more recent information that may not exist inside its static document knowledge base.

## 🧹 Search Result Processing

Raw search results can contain unnecessary information such as timestamps and unrelated metadata.

PRUHelper AI includes text processing logic to clean this information before sending it to the language model.

The processing pipeline can:

* Remove unnecessary timestamps
* Remove metadata noise
* Detect important sentences
* Identify policy related keywords
* Extract policy update dates
* Preserve relevant source information

This helps reduce irrelevant information before response generation.

## 📅 Policy Date Extraction

The prototype contains logic for identifying dates associated with policy changes.

Examples include phrases such as:

```text
Updated on...
Effective from...
Announced...
Implemented...
As of...
Since...
```

These dates can provide additional context when answering questions involving financial or insurance policy changes.

## 🏥 Insurance & Healthcare Queries

The prototype was also designed to handle healthcare and insurance related scenarios.

Queries containing concepts such as:

* Hospital treatment
* Medical emergencies
* Insurance coverage
* Claims
* Panel hospitals
* PRUShield
* PRUExtra
* Co-payment

can trigger additional query context intended to improve the relevance of retrieved information.

## 💬 Example Query

A user could ask:

```text
What are the latest CPF policy changes in Singapore?
```

or:

```text
Which hospitals are covered under my insurance plan?
```

PRUHelper AI would attempt to retrieve relevant information from its knowledge base before falling back to web search when required.

## 🏗️ Relationship to PRUClarity / Clarity+

PRUHelper AI was not developed as an independent final product.

It was created as one of the proposed features within **PRUClarity** during the **PolyFinTech100 API Hackathon 2025**.

```text
PolyFinTech100 API Hackathon 2025
              ↓
          PRUClarity
              ↓
       PRUHelper AI
       Feature Prototype
              ↓
     Feature Later Removed
              ↓
          Clarity+
```

As the product evolved, PRUClarity was renamed **Clarity+** and PRUHelper AI was removed from the final feature set.

This repository therefore represents an earlier stage of the project's development and is preserved as a technical showcase.

## 🛠️ Technology Stack

| Technology    | Purpose                         |
| ------------- | ------------------------------- |
| Python        | Core application development    |
| Streamlit     | User interface                  |
| OpenAI        | Language model responses        |
| LlamaIndex    | RAG and AI tooling              |
| FastEmbed     | Document embeddings             |
| Google Search | Live information retrieval      |
| PyMuPDF       | PDF document processing         |
| python dotenv | Environment variable management |

The repository dependencies include Streamlit, OpenAI, LlamaIndex, FastEmbed, Google Search and PyMuPDF.

## 📁 Project Structure

```text
PRUHelper-AI/
│
├── app.py
│   └── Main Streamlit application
│
├── tools.py
│   ├── RAG pipeline
│   ├── Google Search
│   ├── Search result processing
│   └── AI response generation
│
├── config.py
│   └── Application and model configuration
│
├── styles.py
│   └── Streamlit styling
│
├── utils.py
│   └── Shared interface utilities
│
├── docs/
│   └── PDF knowledge base
│
├── requirements.txt
├── .gitignore
└── README.md
```

## 🚀 Installation

### Prerequisites

Make sure you have installed:

* Python 3
* pip
* An OpenAI API key

### 1. Clone the Repository

```bash
git clone https://github.com/khosoongyang/PRUHelper-AI.git
```

Enter the project directory:

```bash
cd PRUHelper-AI
```

### 2. Create a Virtual Environment

#### Windows

```powershell
python -m venv venv
venv\Scripts\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project directory.

Add your OpenAI API key:

```env
OPENAI_API_KEY=your_openai_api_key
```

Do not commit your `.env` file or API keys to GitHub.

### 5. Add Knowledge Base Documents

PDF documents can be placed inside:

```text
docs/
```

The application will attempt to load documents from this directory and create a vector index for retrieval.

If no documents are available, the system can continue using its web search functionality.

### 6. Start the Application

```bash
streamlit run app.py
```

Streamlit will display the local application address in your terminal.

## 🧱 Architecture

```text
                    ┌─────────────────┐
                    │      User       │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │    Streamlit    │
                    │       UI        │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │ PRUHelper Tools │
                    └────────┬────────┘
                             │
                ┌────────────┴────────────┐
                │                         │
                ▼                         ▼
       ┌────────────────┐       ┌─────────────────┐
       │ PDF Knowledge  │       │  Google Search  │
       │     Base       │       │    Fallback     │
       └───────┬────────┘       └────────┬────────┘
               │                         │
               ▼                         ▼
       ┌────────────────┐       ┌─────────────────┐
       │ Vector Search  │       │ Result Cleaning │
       └───────┬────────┘       └────────┬────────┘
               │                         │
               └────────────┬────────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │     OpenAI      │
                   │      LLM        │
                   └────────┬────────┘
                            │
                            ▼
                   ┌─────────────────┐
                   │ Structured      │
                   │ User Response   │
                   └─────────────────┘
```

## 🎯 Project Purpose

PRUHelper AI was developed to explore how AI could simplify the process of understanding complex financial and insurance information.

The prototype combined several concepts:

* Generative AI
* Retrieval Augmented Generation
* Semantic retrieval
* Web search
* Financial information discovery
* Insurance information
* Document processing
* Prompt engineering
* Natural language interfaces

The project also provided an opportunity to explore how AI functionality could be integrated into a broader FinTech product rather than operating as a standalone chatbot.

## 🧪 Project Status

**PRUHelper AI is no longer an active feature of Clarity+.**

The repository is maintained as an archive and portfolio showcase of a feature explored during the development of PRUClarity for the PolyFinTech100 API Hackathon 2025.

The implementation may therefore contain experimental logic, assumptions, or integrations that were appropriate for the prototype but are not representative of the current Clarity+ platform.

## ⚠️ Disclaimer

PRUHelper AI is an experimental prototype and should not be treated as a source of professional financial, medical, or insurance advice.

Information generated by AI systems may be incomplete or inaccurate and should be verified against authoritative sources.

## 🔮 What I Learned

The prototype explored practical challenges involved in building AI powered financial information systems, including:

* Combining internal documents with external information
* Choosing between RAG and web search
* Cleaning search results before LLM processing
* Structuring AI responses for users
* Designing fallback behaviour
* Building financial information interfaces
* Integrating an AI feature into a wider FinTech product

---

Originally developed as an experimental feature of **PRUClarity**, now **Clarity+**, during the **PolyFinTech100 API Hackathon 2025**.
