# LLM Website Summarizer

A Python-based application that extracts content from a website and uses a Large Language Model (LLM) to generate a concise, readable summary.

The project demonstrates a practical Generative AI workflow that combines web scraping, prompt engineering, and OpenAI API integration.

## Overview

Reading long web pages can be time-consuming. This project explores how an LLM can help users understand website content more quickly by converting extracted text into a short summary.

The user provides a website URL. The application retrieves its content, constructs a prompt, sends the content to an OpenAI language model, and returns the generated summary.

## Features

- **URL-based content extraction:** Retrieve website content using a dedicated Python scraping module.
- **LLM-powered summarization:** Generate concise summaries using OpenAI's chat completions API.
- **Prompt engineering:** Separate system instructions from user-provided website content.
- **Configurable summarization behavior:** Modify the system prompt to adjust the summary's tone and instructions.
- **Markdown output:** Display generated summaries in a readable format within a Jupyter notebook.
- **Multiple website experiments:** Test the workflow against different websites, subject to their accessibility and scraping compatibility.

## How It Works

The application follows a simple pipeline:

1. **Input:** Provide a website URL.
2. **Extraction:** Call `fetch_website_contents(url)` from `scraper.py` to retrieve the website text.
3. **Prompt construction:** Combine the system prompt and extracted content using `messages_for(website)`.
4. **LLM inference:** Send the messages to the OpenAI API using the `gpt-4.1-mini` model.
5. **Output:** Return the generated summary and optionally render it as Markdown.

## Technical Implementation

### 1. Website Content Extraction

The notebook imports the scraping function:

```python
from scraper import fetch_website_contents

website = fetch_website_contents("https://example.com")
print(website)
```

The scraper is responsible for retrieving the website content before it is passed to the language model.

### 2. Prompt Engineering

The application uses a system prompt to define the summarization assistant's behavior and a user prompt to provide the extracted content.

This separation allows the summarization instructions to be modified independently of the website being analyzed.

### 3. OpenAI API Integration

The application sends the constructed messages to the selected model:

```python
response = openai.chat.completions.create(
    model="gpt-4.1-mini",
    messages=messages_for(website)
)
```

The generated summary is retrieved from the first response choice.

### 4. End-to-End Summarization

The `summarize(url)` function connects the extraction and generation stages, providing a single function for summarizing a website.

The `display_summary(url)` helper displays the returned summary using IPython Markdown.

## Technology Stack

- **Python** — application logic and workflow orchestration
- **Jupyter Notebook** — interactive development and experimentation
- **OpenAI API** — language-model inference and text summarization
- **Prompt engineering** — control over the model's summarization behavior
- **python-dotenv** — loading configuration from environment variables
- **IPython Markdown** — formatted output inside the notebook

The precise dependencies used internally by `scraper.py` should be documented once that file is included.

## Prerequisites

- Python installed on your system
- Jupyter support in your IDE or a Jupyter environment
- An OpenAI API key with access to the selected model
- The project files, including `scraper.py`

API usage may incur charges depending on your account and model pricing.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/llm-website-summarizer.git
cd llm-website-summarizer
```

Replace `YOUR_GITHUB_USERNAME` with your GitHub username.

### 2. Create a virtual environment

Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, use Command Prompt:

```bat
.venv\Scripts\activate.bat
```

### 3. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 4. Configure your API key

Create a `.env` file in the project root:

```dotenv
OPENAI_API_KEY=your_openai_api_key_here
```

Replace the placeholder with your own key.

Never commit your `.env` file or expose your API key in a notebook, source file, screenshot, or GitHub commit.

### 5. Run the notebook

Start Jupyter:

```bash
jupyter notebook
```

Open `day1.ipynb`, select the project's Python environment as the kernel, and run the cells from top to bottom.

### 6. Summarize a website

Use the summarization function with a URL:

```python
summary = summarize("https://example.com")
print(summary)
```

You can also display the output in Markdown:

```python
display_summary("https://example.com")
```

## Limitations

- Not every website can be scraped successfully.
- Websites that rely heavily on client-side JavaScript may not expose their content to a simple scraper.
- Some websites restrict automated requests or return access-denied responses.
- The quality of a summary depends on the extracted text, prompt instructions, and language model.
- Very long pages may require text cleaning or truncation to fit model context limits.
- LLM-generated summaries can omit details or contain inaccuracies; verify important information against the original source.

## Security and Responsible Use

- Keep API keys in environment variables and exclude `.env` from version control.
- Respect website terms of service, robots.txt guidance, rate limits, and applicable copyright requirements.
- Do not use the application to bypass authentication or access controls.
- Treat generated summaries as AI-produced interpretations of the original content.

## Future Improvements

Potential extensions include:

- A simple Streamlit or web-based user interface
- Better extraction of article text and metadata
- Support for JavaScript-rendered websites
- URL validation, request timeouts, and clearer error handling
- Text cleaning and chunking for long pages
- Adjustable summary length and output style
- Unit tests and automated code-quality checks

## License

Choose and add an appropriate open-source license before distributing the project. If the notebook is adapted from an existing course, check the original course's licensing and attribution requirements before publishing adapted material.

---

**Built with Python and OpenAI to explore practical LLM-powered text summarization.**