# Kaiboard Use Cases and Features

## Core Use Cases
-   **Offline Dictation**: Transcribe speech to text without an internet connection.
-   **Privacy-First Typing**: Sensitive voice data never leaves the device.
-   **Multilingual Support**: Support for various languages via specific Whisper models.
-   **Hands-Free Input**: Useful for accessibility and driving modes.
-   **Secure Comms**: Dictating sensitive Signal messages offline.
-   **Journaling**: Voice-to-text in Notes apps without data syncing.
-   **Technical Dictation**: Using custom vocabularies/models.

## Key Features
-   **Whisper.cpp Integration**: State-of-the-art accuracy on mobile.
-   **Real-time Transcription**: (Experimental) Partial results displayed as you speak.
-   **Customizable Models**: Users can load `tiny`, `base`, or `small` models based on device capability.
-   **Modern UI**: Built with Jetpack Compose.
-   **Model Management**: User-selectable performance vs accuracy profile.

## Enhancements

### Visual Customization (Typeless Style)
-   **Aesthetic**: Minimalist, distraction-free interface.
-   **Visualization**: Waveform or confident text streaming.

### Local LLM Integration (Implemented)
-   **Feature**: "Refine with AI" button on the keyboard.
-   **Workflow**:
    1.  User dictates text via Whisper.
    2.  User taps the "Magic Star" button.
    3.  App sends current text/context to the configured Local LLM endpoint (default: `http://10.0.2.2:11434/api/generate` for Android Emulator access to host Ollama).
    4.  LLM (e.g., Llama 3) processes the text to fix grammar and clarity.
    5.  Original text is replaced with the refined version.
-   **Configuration**:
    -   Users can set the LLM API URL in the App Settings.
    -   Default supports Ollama/OpenAI-compatible JSON endpoints.
