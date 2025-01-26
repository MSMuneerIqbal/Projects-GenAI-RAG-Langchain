# Video Analysis using Langchain and Gemini

This notebook demonstrates how to analyze an AI-generated video using Langchain and Google's Gemini models. It takes a video file path as input, extracts key visual information, including scene descriptions and any spoken text, and then presents this data in a JSON format.

## Key Concepts

1.  **Setup and Installation**:
    *   The notebook begins by installing the necessary libraries using `pip`:
        *   `langchain`: A framework for building applications with language models.
        *   `google-genai`: Google's Gemini API wrapper.
        *   `langchain-google-genai`: Langchain integration for Google's Generative AI models.

2.  **Importing API Key**:
    *   The notebook retrieves the Google API key from Google Colab's secrets using `google.colab.userdata`.
    *   This API key is then set as an environment variable for use with the Gemini model.

3.  **Importing Libraries**:
    *   The notebook imports necessary modules from the installed libraries:
        *   `ChatGoogleGenerativeAI`: For interacting with Google's Gemini models.
        *   `ChatPromptTemplate`: For creating structured prompts for the language model.
        *   `JsonOutputParser`: For parsing the language model's output into JSON format.
        *   `SystemMessage`: For defining system-level instructions within prompts.
        *   `json`: For handling JSON data.
        *   `os`: For handling environment variable.

4.  **`analyze_video_with_langchain` Function**:
    *   This function encapsulates the entire video analysis process.
    *   **Model Initialization**: It initializes a `ChatGoogleGenerativeAI` model using Gemini `gemini-2.0-flash-exp` along with the API key.
    *   **Prompt Definition**: It constructs a structured prompt for the LLM:
        *   A system message sets the context for the LLM, instructing it to act as an expert video analyzer.
        *   A human message defines the specific information to extract, such as scene timecodes, visual descriptions, and spoken text. It instructs the LLM to output a JSON array with the required keys, and to use `null` if no spoken text is present.
    *   **Chain Creation**: It creates a chain that links the prompt, LLM, and JSON parser together. The `|` operator is used to chain them in a sequence.
    *   **Chain Execution**: It invokes the chain with the video path and captures the model output.
    *   **Error Handling**: It includes a try-except block to gracefully handle potential errors and return `None` if an error occurs.

5.  **Main Execution Block**:
    *   This block:
        *   Specifies the video file path, which is set to `/content/butterfly_journey.mp4`.
        *   Calls the `analyze_video_with_langchain` function.
        *   Prints the analysis results if successful or a failure message if an error occurred.

## How it Works

1.  **Setup**: The notebook sets up the required environment by installing libraries and importing the API key.
2.  **Prompt Engineering**: A carefully crafted prompt is designed to guide the LLM in analyzing the video. The prompt instructs the model on its role, the data to extract, and the desired output format.
3.  **Video Analysis**: The video file path is passed to the LLM using the specified prompt. The model processes the video's content and identifies distinct scenes, extracting the required information about visual descriptions and spoken text.
4.  **Output Generation**: The model generates output as a JSON array of objects, with each object containing the scene timecode, visual description, and spoken text.
5.  **Output Presentation**: The JSON output is printed to the console in a nicely formatted manner.

## Usage

1.  Ensure that you have the necessary libraries installed.
2.  Obtain a Google API key and set it as a secret in your Colab environment using `google.colab.userdata`.
3.  Upload your video file to the Colab environment.
4.  Modify the `video_file_path` variable if your video file has a different name or is located in a different directory.
5.  Run the cells of the notebook sequentially.
6.  The JSON analysis results will be printed to the console.

This notebook provides a basic framework for video analysis. You can further expand its functionality by adding more detailed video analysis parameters, integrating it with other video-processing libraries, or saving the output to different file formats.