# Kaiboard Technology Architecture

## Technology Stack

| Layer | Technology | Description |
|-------|------------|-------------|
| **UI Layer** | Jetpack Compose | Modern, declarative native UI for Android. |
| **Service Layer** | Kotlin | Android InputMethodService implementation. |
| **Bridge Layer** | JNI (Java Native Interface) | Communication between Java/Kotlin and C++. |
| **Core Engine** | C++ (whisper.cpp) | High-performance inference engine for Whisper models. |
| **Model Format** | GGML / GGUF | Quantized binary format for efficient edge inference. |
| **Build System** | Gradle + CMake | Android build toolchain integrating C++ compilation. |

## Platform and Infrastructure Requirements

### Running Whisper.cpp Locally
To run variants of Whisper.cpp locally on a phone or laptop:

#### Android
*   **Hardware**: ARM64 processor.
*   **RAM**: At least 4GB (Tiny/Base models), 8GB recommended for larger models.

#### Laptop
*   **Hardware**: Modern CPU (AVX2 support) or GPU (Metal on Mac, CUDA on Linux/Windows).

### Models
*   Must be converted to `ggml` or `gguf` format.
*   **Common variants**:
    *   `tiny.en` (75MB)
    *   `base.en` (142MB)
    *   `small.en` (466MB)
*   **Quantization**: `q4_0`, `q5_0`, `q8_0` reduce memory usage with minimal accuracy loss.
