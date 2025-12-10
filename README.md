# Dictation web app 
A fully local, privacy-focused dictation and text-cleanup web application powered by Whisper (local speech-to-text), FastAPI, and Ollama (local LLMs like Mistral). The app allows users to record audio, transribe it, clean up text, and download results as a PDF, all without sending data to external servers. 

## Features
- Local speech-to-text using Whisper
- Optional text cleanup using Mistral via Ollama
- Privacy-first (audio never leaves your machine)
- Option to parse audio into template of chosen paper format
- PDF generation using FPDF 
- Basic UI with dictation controls
- Expandable architecture for accessibility

## Project Structure
project/ <br>
│── app/ <br>
│   ├── api/
│   │   └── app.py            # FastAPI backend endpoints
│   ├── services/
│   │   ├── audio_utils.py    # Handles audio conversion
│   │   ├── math.py           # Used to create math equations
│   │   └── whisper.py        # Loads Whisper model and transcribes audio
│   ├── static/
│   │   ├── css/
│   │   │   └── styles.css    # Frontend styling
│   │   ├── js/
│   │   │   ├── main.js       # Frontend JS for main page
│   │   │   └── paper.js      # Frontend JS for paper template page
│   │   └── sounds/           # Audio assets for frontend
│   ├── templates/
│   │   ├── clean.html
│   │   ├── dictation.html
│   │   ├── index.html
│   │   ├── paper.html
│   │   └── formats/          # JSON files to dynamically create paper sections
│   └── tests/                # Unit and integration tests
│── requirements.txt           # Python dependencies
│── README.md                  # Project documentation

## Installation
1. **Clone project:**  
    'git clone <repo_url>'
    'cd <project_folder>'

2. **Install dependencies:**  
    'pip install -r requirements.txt'
If you add new packages during development:
    'pip freeze > requirements.txt'

3. **Running the Application Locally**
    1. In one terminal start ollama REST API:
        * Ollama must be running before the backend can communicate with Mistral
            'ollama serve'
        * This exposes a local REST API at:
            'http://localhost:11434'
    2. Start the backend (FastAPI + Whisper)
        * In another terminal, start backend API (FastAPI + Whisper):  
                'uvicorn app.main:app --reload'
          The backend automatically serves the frontend as well.
        * App runs at port 8000
        * Visit 'http://localhost:8000' to test web app! 
    * **Optional:** To view frontend files seperately run: 
            'python3 -m http.server 5500'  
        * Then visit http://localhost:5500 

**Note:**  
Frontend is served on localhost:5500  
Backend is served on localhost:8000 

## Whisper
Whisper is being run locally beacause it is free and open-source. It also allows for privacy, meaning audio will not leave our server and your data will not be sent to OpenAI. Running Whisper locally also allows us to add segmenting. Meaning we can add built in equation builders. 

## Local LLM Cleanup (Ollama)
Ollama is a tool that lets users run LLMs locally on your machine. Ollama manages model downloads, version, and execution for you, making it easier to work with LLMs without dealing with complex setup.  
1. **Install Ollama**  
    **macOS:** 'brew install ollama'  
    **Windows:**  
    * Visit 'https://ollama.com/download'
    * Download and run the .exe installer
2. **After installation, open command prompt and run:**  
    Run REST API via: 'ollama serve'  
    
Local REST API at: 'http://localhost:11434'
Responses generated at: 'http://localhost:11434/api/generate'

### Mistral Via Ollama
Mistral, developed by Mistral AI team, is the specific LLM we chose to use for text cleanup. It is an advanced model designed for natural language tasks. 
    **Download Mistral**
        'ollama pull mistral'

##### kill Ollama
Find Process: lsof -i :11434
Kill Process: kill [PID]

#### Sounds from freesound.org

### Download text into PDF
Sending plain text to backend to locally convert to PDF via FPDF (python library)  
PDF file is generated and saved locally on the server and streamed to client  

## Customization
FPDF allows for easy customization of the PDF on the backend to create pdfs that look like a academic paper, research artical, or formal document, etc.  
Creating PDFs on the backend also allows us to easily add images or tables into the text. It also allows for the customization of font style and sizes.  

FPDF allows you to add headers or footers unlike if you did it on the frontend.
