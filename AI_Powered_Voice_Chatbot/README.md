# Voice-to-Voice Chatbot with Groq, Whisper, and gTTS

This Python script implements a voice-to-voice chatbot using several key technologies:

*   **Whisper:** For transcribing speech to text.
*   **Groq:** For generating responses using a large language model (LLM).
*   **gTTS (Google Text-to-Speech):** For converting text responses back into speech.
*   **Gradio:** For creating an interactive user interface.

## Key Concepts

1.  **Libraries**:
    *   `os`: For interacting with the operating system (not directly used in this version).
    *   `gradio`: For creating the user interface.
    *   `whisper`: For speech-to-text transcription.
    *   `gtts`: For text-to-speech conversion.
    *   `groq`: For accessing the Groq API and using LLMs.

2.  **Groq API Setup**:
    *   The script initializes a `Groq` client with your API key. **Note:** You must replace `"Enter your groq api key"` with your actual Groq API key for the script to work.

3.  **Whisper Model Loading**:
    *   The `whisper.load_model("base")` line loads the "base" version of the Whisper speech-to-text model. This model is used to transcribe audio into text.

4.  **`chatbot` Function**:
    *   This is the core function of the application. It handles the entire process of converting speech to text, generating a response, and converting the response back to speech:
        *   **Transcription:** The `model.transcribe(audio)` function uses Whisper to convert the input audio file to text.
        *   **LLM Response Generation:** The `client.chat.completions.create` function uses the Groq API with the `llama3-8b-8192` model to generate a response based on the transcribed text. The model's response is extracted from `chat_completion.choices[0].message.content`.
        *   **Text-to-Speech:** The `gTTS` is used to convert the generated text response into an audio file named "response.mp3".
        *   **Return values:** It returns the response text and the path to the generated audio file.

5.  **`build_interface` Function**:
    *   This function builds the Gradio interface:
        *   It defines the layout of the user interface with a title and description using markdown.
        *   It creates an audio input component using `gr.Audio(type="filepath", label="Record Your Voice")` which allows user to record the voice.
        *   It creates a text box (`gr.Textbox`) to display the chatbot's response and audio output using (`gr.Audio`) to play the response in audio format.
        *   It creates a "Submit" button which triggers the `chatbot` function when clicked. It maps the audio input to the `chatbot` function and displays its results in the text box and audio output components.
        *   Returns the constructed `gr.Blocks()` object.

6. **Main Execution Block**:
   *   This block:
      * Calls `build_interface` to create a gradio interface.
      * launches the gradio interface using `interface.launch()`.

## How it Works

1.  **User Input**: The user interacts with the Gradio interface by recording their voice through the audio input component.
2.  **Transcription**: When the "Submit" button is clicked, the recorded audio is passed to the `chatbot` function, where it's transcribed into text using the Whisper model.
3.  **Response Generation**: The transcribed text is sent to the Groq API, using the Llama 8B LLM, to generate a text-based response.
4.  **Text-to-Speech Conversion**: The text response is then converted into an audio file using gTTS.
5.  **Output**: The text response and the audio file path are returned and displayed in their respective output components on the Gradio interface.

## Usage

1.  Ensure that you have the required libraries installed: `gradio`, `whisper`, `gtts`, and `groq`.
2.  Replace `"Enter your groq api key"` with your actual Groq API key.
3.  Run the script.
4.  A Gradio interface will launch in your browser.
5.  Record your voice input and click "Submit" to interact with the chatbot.

This script provides a basic framework for building a voice-to-voice chatbot. You can further expand its functionality by improving the prompt to LLM, adding context awareness or integrating with other services.

**Note:**
* Ensure you have a valid Groq API key.
* This implementation uses the base whisper model, which may not perform as well as large models. If you want higher accuracy, you may try larger whisper models.
* Make sure you have `ffmpeg` or `libav` installed if you face problems playing the audio files in the UI.