
@echo off
title CreatorPilot AI - Automatic Setup
color 0A

echo ========================================
echo       CREATORPILOT AI INSTALLER
echo ========================================
echo.

:: Check Python
python --version
if errorlevel 1 (
    echo Python not installed. Install Python first:
    echo https://www.python.org/downloads/
    pause
    exit /b
)

:: Create project folder
if not exist CreatorPilot-AI mkdir CreatorPilot-AI
cd CreatorPilot-AI

:: Create app.py if it does not exist
if not exist app.py (
    echo.
    echo Create app.py in this folder and paste the complete
    echo CreatorPilot AI Python code into it.
    notepad app.py
    echo Save app.py and close Notepad.
    pause
)

:: Create virtual environment
if not exist .venv (
    python -m venv .venv
)

:: Activate environment
call .venv\Scripts\activate.bat

:: Install dependencies
python -m pip install --upgrade pip
pip install streamlit requests

:: Check Ollama
where ollama >nul 2>&1
if errorlevel 1 (
    echo.
    echo Ollama is not installed.
    echo Install it from https://ollama.com/download/windows
    pause
    exit /b
)

:: Download model
ollama pull llama3.2:3b

:: Launch application
echo.
echo ========================================
echo       STARTING CREATORPILOT AI
echo ========================================
streamlit run app.py

pause
