

# MACHINE LEARNING
## Amazon Comprehend
Amazon Comprehend is a natural-language processing (NLP) service that uses machine learning to uncover valuable insights and connections in text.
- input document and it parses and develops insights (like name, addresses, PII, phrases, common elements, sentiment)
- pre-trained or custom models
- realtime for small workloads, async for larger workloads
- confidence 0.0 - 1.0 (1 being wholly confident)

## Amazon Kendra
Amazon Kendra is an intelligent search service powered by machine learning (ML).
- designed to mimic interacting with a human expert
- suppports wide range of question types: factoid, descriptive, keyword
- Kendra is a backend service that you'd API-integrate with your app for search functionality
### Kendra Concepts
- Index. Searchable data
- Data source. Where your data lives; S3, Google Workspace, RDS, Salesforce, FSx, etc etc
- Documents. Structured and unstructured indexable items

## Amazon Lex
Amazon Lex is a fully managed artificial intelligence (AI) service with advanced natural language models to design, build, test, and deploy CONVERSATIONAL interfaces in applications.
- interactive chat bots
- backend service that you'll use to add capabilities to your application
- POWERS THE ALEXA SERVICE
- Automatic Speesh Recognition (ASR); sppech-to-text, Natural Language Understanding (NLU); intent,
- Chatbots, Voice Assistance, Q&A Bots, Phone bots

## Amazon Polly
Amazon Polly is a service that turns text into lifelike speech text to speech TTS), allowing you to create applications that talk, and build entirely new categories of speech-enabled products.
- polly - parroting text to speech. NO TRANSLATION
- two types of TTS.. .standard and neural. Standard concatenates phenomes, neral much more complex but more natural

## Amazon Rekognition
Amazon Rekognition offers pre-trained and customizable computer vision (CV) capabilities to extract information and insights from your IMAGES and VIDEOS.
- deep learning based
- ID objects, people, text, activities, face detection/analysis/comparison, pathing, much more
- Can analyze live video by integrating with kinesis video streams

## Amazon Textract
Amazon Textract is a machine learning (ML) service that automatically extracts text, handwriting, and data from scanned documents. It goes beyond simple optical character recognition (OCR) to identify, understand, and extract data from forms and tables
- input documents = JPG, PNG, PDF, TIFF
- output: extracted text, structure, and analysis
- types of analysis: document, receipts, identity documents
- backend style service that can be intergrated with your apps or with other AWS services

## Amazon Transcribe
Amazon Transcribe is an automatic speech recognition (ASR) service that uses machine learning models to convert audio to text. You can use Amazon Transcribe as a standalone transcription service or to add speech-to-text capabilities to any application.
- input Audio, output Text
- Use Cases: full text indexing to allow searching of audio, create meeting notes, subtitles/captions/transcripts
-- call analytics (sentiment, characteristics, etc)

## Amazon Translate
Amazon Translate is a neural machine translation service that delivers fast, high-quality, affordable, and customizable language translation.
- one word at a time translation and outputs semantic representation or meaning, decorder reads meaning and writes target language
- backend style service that integrates with other services/apps/platforms

## Amazon Forecast
Amazon Forecast is a fully managed service that uses statistical and machine learning algorithms to deliver highly accurate time-series forecasts.
- Predicting retail demand, supply chain, staffing, web traffic.
- Import historical & related data, understand what's normal, output forecasts and forecast explainability
- backend style service that integrates with your apps or you can use web console, CLI. And APIs, Python SDK

## Amazon Fraud Detecto
Amazon Fraud Detector is a fully managed fraud detection service that automates the detection of potentially fraudulent activities online. These activities include unauthorized transactions and the creation of fake accounts. Amazon Fraud Detector works by using machine learning to analyze your data.
- online fraud, transactional fraud, account takeover (phishing etc)
- backend style service that integrates into your apps

## Amazon SageMaker
Amazon SageMaker is a fully managed machine learning service. With SageMaker, data scientists and developers can quickly and easily build and train machine learning models, and then directly deploy them into a production-ready hosted environment.
- implementation of a fully managed ML service: fetch, clean, prepare, train, eval, deploy, monitr/collect -- the whole ML lifecycle
- SageMager Studio - Dev environment for the ML lifecycle
- SageMaker Domain - olation or groupings / container for a project
- Containers. Docker containers deployed to ML EC2 instances
- Hosting. Can host ML models
- SageMaker has no cost, the resources it creates do

## AWS Local Zones
AWS Local Zones are a type of infrastructure deployment that places compute, storage, database, and other select AWS services close to large population and industry centers.
- physical distance affects latency and performance. AWS Local Zones brings infrastructure physically closer for super low latencies
- Local Zones support DX (direct connect)
- Local Zones have Private networking with their parent region
- Not all products support Local Zones
- HIGHEST PERFORMANCE REQUIRED? Local Zones
