# PDF Invoice Information Extraction using Language Models

## Overview

This project automates the extraction of key information from invoice PDF documents using advanced natural language processing (NLP) models. It leverages state-of-the-art language models to interpret the contents of an invoice and extract important fields such as invoice number, date, seller and buyer information, list of items, and totals.

The project is designed to handle a wide variety of invoice formats and terminologies by using flexible models that understand context and language, making it adaptable to different invoicing conventions and document structures.

## Essence of the Project

Manually extracting data from invoices is a time-consuming and error-prone task, especially when dealing with large volumes of invoices that can differ greatly in format. The goal of this project is to create an intelligent, automated system that can:
- Extract relevant fields from various invoice formats.
- Adapt to changing terminologies (e.g., 'buyer' could be 'customer' or 'client').
- Generate structured output such as JSON or CSV, making the data ready for further processing or storage in databases.

The core essence of this project lies in **automating repetitive data entry tasks** through AI, making invoice data extraction **faster, more accurate, and scalable**.

## Features

- **Flexible Extraction**: Extracts core fields such as invoice numbers, dates, client and seller details, line items, and totals.
- **Adaptable Models**: Supports different invoice layouts by utilizing language models that can adapt to a variety of formats and terminologies.
- **Customizable Prompts**: Allows users to define system prompts to extract specific information according to their needs.
- **Batch Processing**: Supports batch processing of multiple PDF files, making it suitable for high-volume invoice extraction tasks.
- **Embeddings for Document Search**: Utilizes vector embeddings for efficient document search and retrieval within the context of invoice data.

## Why This Project Matters

1. **Efficiency**: Reduces the time spent on manual data entry, particularly for organizations that deal with hundreds or thousands of invoices daily.
2. **Accuracy**: Minimizes human error in data extraction by leveraging language models trained on a wide range of document types.
3. **Scalability**: Capable of processing a large number of invoices in parallel, making it suitable for both small businesses and large enterprises.
4. **Adaptability**: Can be customized for various industries, as it allows flexibility in recognizing different labels and field names across invoices.

## Technical Workflow

1. **Load the Model and Tokenizer**  
   The project uses `AutoGPTQ` models, optimized for both speed and accuracy. The model and tokenizer are loaded once and can be reused throughout the processing pipeline.

   ```python
   model, tokenizer = load_model_and_tokenizer()

2. **PDF Loading and Parsing**  
   PDFs are processed using `PyPDFLoader` to extract the raw text, which is then passed to the language model for further analysis. The text is split into meaningful sections using embeddings, making it easier for the model to focus on relevant content.

3. **Information Extraction**  
   The language model, guided by predefined prompts, extracts relevant fields from the parsed text. Prompts can be adjusted based on the specific format or terminology used in the invoice.

4. **Data Storage**  
   The extracted data is stored in a structured format (JSON or CSV). Each document's output includes:
   - **Invoice Number**
   - **Invoice Date**
   - **Seller Name, Address, and Contact Information**
   - **Client Name, Address, and Contact Information**
   - **Itemized List of Products/Services**
   - **Subtotal, Taxes, and Grand Total**

   Example structure:

   ```json
   {
       "invoice_number": "12345",
       "invoice_date": "2024-10-18",
       "seller_name": "ABC Corp",
       "client_name": "XYZ Ltd",
       "items": [
           {"description": "Product 1", "quantity": 2, "price": 100.00},
           {"description": "Product 2", "quantity": 1, "price": 200.00}
       ],
       "subtotal": 400.00,
       "tax": 40.00,
       "grand_total": 440.00
   }
   ```

5. **Embedding and Indexing for Search**  
   In addition to extracting data, the project also supports embedding the text for indexing. This allows for efficient querying and retrieval of relevant invoice data in large datasets. It uses `HuggingFaceInstructEmbeddings` and `Chroma` for managing these vectorized representations.

6. **Processing Multiple PDFs**  
   To handle large datasets, the project can process multiple PDF files simultaneously, extracting relevant information from each file and saving the results for easy access.

   ```python
   process_all_pdfs(pdf_folder_path, model, tokenizer)
   ```

## Model Used: Llama-2-13B-Chat-GPTQ

For the core language model, this project leverages **Llama-2-13B-Chat-GPTQ**, a highly advanced, efficient, and optimized large language model (LLM) from Meta AI.

### About Llama-2-13B-Chat

**Llama-2** is a powerful series of open-access large language models developed by Meta AI. The 13B variant refers to the model having 13 billion parameters, making it one of the more capable models in terms of understanding context, language nuances, and text generation while remaining efficient enough for practical applications.

Llama-2 models are built to be conversational agents, capable of understanding and generating human-like text based on context. For this project, the chat variant is especially beneficial because it is fine-tuned to handle dialogues and inquiries in natural language, which is perfect for tasks like parsing unstructured documents (like invoices) where context and accurate field extraction are critical.

### Model Used: Llama-2-13B-Chat-GPTQ

Leveraging Meta AI's Llama-2-13B-Chat-GPTQ model, we benefit from:
- **Powerful Context Understanding**: 13 billion parameters for effective extraction.
- **Efficiency**: Optimized for faster processing on standard hardware.
- **Flexibility**: Adapts to different invoice terminologies.

## How to Use

1. **Load the Model**: Load the model and tokenizer once to prepare the pipeline.

   ```python
   model, tokenizer = load_model_and_tokenizer()
   ```

2. **Process a Single PDF**: To process a single invoice:

   ```python
   result = process_pdf("path/to/invoice.pdf", model, tokenizer)
   ```

3. **Process Multiple PDFs**: For batch processing of multiple invoices:

   ```python
   process_all_pdfs("path/to/pdf_folder", model, tokenizer)
   ```

4. **Review Output**: The extracted data will be saved in structured JSON files for each PDF, making it easy to review or upload to a database.


## Future Improvements

- **Invoice Template Learning**: Train models to recognize new invoice templates on the fly.
- **Enhanced Item Parsing**: Improve the model’s ability to parse complex itemized lists.
- **Multilingual Support**: Expand support for invoices in different languages.
- **API Integration**: Provide REST API access for integrating with other systems such as accounting or ERP platforms.

## Conclusion

By using Llama-2-13B-Chat-GPTQ, this project pushes the boundaries of invoice data extraction automation. The combination of a robust language model and efficient quantization techniques makes it an ideal solution for businesses looking to streamline their invoice processing workflows with minimal manual intervention. This system promises to improve data extraction accuracy, scalability, and adaptability across a wide
