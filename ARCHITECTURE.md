# Kaiboard Architecture

## High-Level Architecture
The application follows a standard Android service architecture, integrating native C++ code via JNI.

```mermaid
graph TD
    User[User] -->|Press Record| UI[VoiceKeyboardView]
    UI -->|Trigger| Service[VoiceKeyboardInputMethodService]
    Service -->|Audio Stream| Recorder[AudioRecorder]
    Service -->|Audio Data| Lib["LibWhisper (Kotlin Wrapper)"]
    Lib -->|JNI Call| Native["whisper.cpp (Native C++)"]
    Native -->|Inference| Model["Whisper Model (.bin)"]
    Native -->|Transcribed Text| Lib
    Lib -->|Callback| Service
    Service -->|Commit Text| IME[InputMethodManager]
    IME -->|Text Input| App[Target Application]
```

## Component Diagram

```mermaid
classDiagram
    class VoiceKeyboardInputMethodService {
        +onStartInputView()
        +toggleRecord()
        +processAudio()
    }
    class VoiceKeyboardView {
        +ComposeUI()
        +RecordButton()
    }
    class LibWhisper {
        +init()
        +start()
        +stop()
    }
    class WhisperContext {
        +long ptr
    }
    
    VoiceKeyboardInputMethodService --> VoiceKeyboardView : Manages UI
    VoiceKeyboardInputMethodService --> LibWhisper : Uses
    LibWhisper --> WhisperContext : Wraps Native Ptr
```

## Sequence Diagram: Transcription Flow

```mermaid
sequenceDiagram
    participant User
    participant View as VoiceKeyboardView
    participant Service as InputMethodService
    participant Wrapper as LibWhisper
    participant Native as Whisper.cpp

    User->>View: Tap Record
    View->>Service: toggleRecord()
    Service->>Wrapper: start()
    Service->>Native: Stream Audio Buffer
    loop Audio Processing
        Native->>Native: Encode & Decode
    end
    Native-->>Wrapper: Segment Text
    Wrapper-->>Service: callback(text)
    Service-->>User: Commit Text to Editor
```
