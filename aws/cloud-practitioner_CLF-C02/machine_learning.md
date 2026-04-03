# Amazon Machine Learning Services

## Amazon Rekognition
- Find objects, people, text, scenes in images and videos using ML
- Facial analysis and facial search to do user verification, people counting
- Create database of "familiar faces" or compare against celebrities
- Use Cases
  - *Labelling*
  - *Content Moderation*
  - *Text Detection*
  - *Face Detection & Analysis*
  - *Face Search & Verification*
  - *Celebrity Recognition*
  - *Pathing (ex: for sports game analysis)

## Amazon Transcribe
- Automatically convert speech to text
- Uses a deep learning process called automatic speech recognition (ASR) to convert speech to text quickly and accurately
- Automatically remove Personal Identifiable Information (PII) using Redaction
- Supports Automatic Language Detection for multi-lingual audio
- Use Cases
  - Transcribe customer service calls
  - automate closed captioning and subtitling
  - generate metadata for media assets to create a fully searchable archive

### AWS Polly
- Turns text to speech using deep learning
- Allowing you to create applications that can talk

### Amazon Translate
- Natural and accurate language translation
- Amazon Translate allows you to localize content - such as websites and applications - for international users, and to easily translate large volumes of text efficiently.

### Amazon Lex and Connect
- Amazon Lex (Same technology that powers Alexa)
  - Automatic speech Recognition (ASR) to convert speech to text
  - Natural Language Understanding to recognize the intent of text, callers
  - Helps build chatbots, call center bots
- *Amazon Connect*
  - Receive calls, create contact flows, cloud-based virtual contact center
  - Can Integrate with other CRM systems or AWS
  - No upfront payments, 80% cheaper than traditional contact center solutions

```mermaid
flowchart LR
  A[Phone call schedule] -->|Call| B[AWS Connect]
  B -->|Stream| C[Lex Intent Recognition]
  C -->|invoke| D[Lambda]
  D -->|Schedule| E[CRM]
```

### Amazon Comprehend
- For Natural Language Processing
- Fully managed and serverless service
- Uses Machine Learning to find insights and relationships in text
  - Language of the text
  - Extracts key phrases, places, people, brands or events
  - Understands how positive or negative the text is
  - Analyses text using tokenization and parts of speech
  - Automatically organizes a collection of text files by topic
- Sample use cases:
  - Analyze customer interactions (emails) to find what leads to a positive or negative experience
  - Create and groups articles by topic that Comprehend will uncover.

### Amazon SageMaker AI
- Fully managed service for developers / data scientists to build ML models
- Typically difficult to do all processes in one place + provision servers
- Machine Learning process (simplified): predicting your exam score

### Amazon Kendra
- Fully managed document search service powered by Machine Learning
- Extract answers from within a document (text, pdf, HTML, PowerPoint, MS Word, FAQs)
- Natural Language search capabilities
- Learn from user interactions/feedback to promote preferred results (Incremental Learning)
- Ability to manually fine-tune search results (importance of data, freshness, custom,...)

### Amazon Personalize
- Fully managed ML-service to build apps with real-time personalized recommendations
- Example: personalized product recommendations/re-ranking, customized direct marketing
  - Example: user bought gardening tools, provide recommendations on the next one to buy
- Same technology used by Amazon.com
- Integrates into existing websites, applications, SMS, email marketing systems
- Implement in days, not months
- Use Cases: retail stores, media and entertainment..

### Amazon Textract
- Automatically extracts text, handwriting, and data from any scanned documents using AI and ML
- Extract data from forms and tables
- Read and process any type of document (PDFs, Images)
- Use Cases:
  - Financial Services (e.g, invoices, financial reports)
  - Healthcare (e.g, medical records, insurance claims)
  - Public Sector (e.g, tax forms, ID documents...)

