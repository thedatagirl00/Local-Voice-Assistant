## Project Description: Local Voice Assistant

This project implements a sophisticated local voice assistant designed for privacy and offline operation. It integrates real-time speech recognition, a powerful local Large Language Model (LLM) for intelligent processing, and text-to-speech capabilities for natural language responses. Unlike many cloud-based solutions, this assistant ensures all data processing remains on your local machine by utilizing Ollama to interact with open-source models like Llama 3.

### Features:

*   **Voice Input (`listen` function)**: Captures audio from the microphone, performing intelligent noise reduction by adjusting for ambient sounds. It then accurately transcribes spoken language into text using Google's Web Speech API, offering a highly responsive and clear input mechanism.
*   **Local LLM Processing (`think` function)**: Employs the `ollama` library to facilitate interaction with a locally-served Large Language Model, such as Llama 3. This critical feature ensures that all conversational processing occurs on your device, guaranteeing data privacy and significantly reducing latency compared to cloud-dependent alternatives.
*   **Text-to-Speech Output (`speak` function)**: Transforms the AI's textual responses into natural-sounding speech using `pyttsx3`. This provides an immersive and auditory conversational experience, with customizable voice properties like speech rate.
*   **Continuous Interaction**: The assistant operates within an intuitive `Listen -> Think -> Speak` loop, enabling seamless, ongoing conversational flow until explicitly terminated.
*   **Graceful Exit**: Includes an easy-to-use command detection (`exit`, `stop`, or `quit`) to allow users to gracefully shut down the assistant without needing to force-quit the application.

### Technologies Used:

*   `speech_recognition`: For robust and accurate voice input and transcription, supporting various speech APIs.
*   `ollama`: A powerful tool for running large language models locally, enabling private and efficient inference with models like Llama 3.
*   `pyttsx3`: A cross-platform text-to-speech conversion library that allows the assistant to 'speak' its responses.
*   `pyaudio`: Provides low-level access to audio input/output streams, essential for the microphone interaction used by `speech_recognition`.
*   `portaudio19-dev`: A system-level dependency required for `pyaudio` to function correctly on Linux-based systems (like Google Colab environments).

### Getting Started

To set up and run your local voice assistant, follow these steps:

1.  **Install System Dependencies (Google Colab/Linux)**:

    If you are running this in a Google Colab environment or a similar Linux setup, you'll need to install `portaudio19-dev` first for `pyaudio` to build correctly:

    ```python
    import sys
    if 'google.colab' in sys.modules:
        !apt-get install -y portaudio19-dev
    ```

2.  **Install Python Libraries**:

    Install the necessary Python packages using pip:

    ```bash
    pip install speechrecognition ollama pyttsx3 pyaudio
    ```

3.  **Set Up Ollama and Download Llama 3**:

    Ensure Ollama is running on your system. If not, refer to the official [Ollama website](https://ollama.com/) for installation instructions. Once Ollama is installed, download the Llama 3 model:

    ```bash
    ollama pull llama3
    ```

### Running the Assistant

After setting up the dependencies and Ollama, you can run the voice assistant by executing the `main` function:

```python
def main():
    print("--- Voice Assistant Started ---")
    speak("Hello, I am ready. You can start speaking.")

    while True:
        user_input = listen()

        if not user_input:
            continue

        if user_input.lower().strip() in ["exit", "stop", "quit"]:
            speak("Goodbye!")
            print("Exiting...")
            break

        ai_response = think(user_input)
        speak(ai_response)

if __name__ == "__main__":
    main()
```

This will start the conversational loop. Speak when prompted, and the assistant will respond. 
