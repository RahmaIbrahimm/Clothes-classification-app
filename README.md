# Clothing Classifier 👕📱

A Flutter mobile app that identifies clothing items from a photo using an **on-device machine learning model** — no API calls, no server round-trip, fully offline inference.

## Overview

The app lets a user take a photo or pick one from their gallery, then runs it through a TensorFlow Lite model trained on the Fashion-MNIST dataset to classify the clothing item (e.g. shirt, dress, shoe) and return a ranked list of predictions with confidence percentages.

The entire ML pipeline — training, TFLite conversion, on-device preprocessing, and inference — runs locally on the device. There's no backend dependency for the classification itself.

## How It Works

1. **Image Input** — user captures a photo with the camera or selects one from the gallery (`file_picker`)
2. **Preview & Feedback** — selected image is previewed in the UI with a success indicator
3. **Preprocessing** — `ImagePreprocessing` resizes the image and converts it into a `Float32List` matching the model's expected input shape/normalization
4. **Inference** — `ModelHandler` loads the TFLite model and runs the processed tensor through it
5. **Results** — predictions are displayed in a ranked dialog (e.g. "T-shirt: 98%") showing the top matches with confidence scores

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Flutter / Dart |
| ML Model | TensorFlow Lite (on-device inference) |
| Dataset | Fashion-MNIST |
| Image Input | Camera + Gallery (`file_picker`) |
| File Handling | `dart:io` |
| Custom Services | `ModelHandler` (model loading & inference), `ImagePreprocessing` (image → tensor) |
| UI | Custom theming (`AppStyles`, `AppColors`), reusable widgets (`CustomElevatedButton`) |

## Project Structure

```
lib/
├── ui/          # Screens (e.g. UploadPic)
├── services/     # ML logic — model_handler.dart
├── utils/        # Image preprocessing, colors, styles, constants
└── model/        # Data classes (e.g. ChosenPicture)
```

## What I Built

- Trained the classification model on Fashion-MNIST and converted it to TensorFlow Lite for mobile deployment
- Wrote the on-device preprocessing pipeline to correctly resize and normalize input images to match the model's expected tensor shape
- Integrated TFLite inference directly into the Flutter app — fully offline, no API dependency
- Built camera and gallery image input, with preview and ranked confidence-score results UI

## Getting Started

```bash
# Clone the repository
git clone <repo-url>
cd clothing-classifier

# Install dependencies
flutter pub get

# Run the app
flutter run
```

### Requirements
- Flutter SDK (stable channel)
- Dart SDK
- Android Studio / Xcode for platform builds
- Camera and storage permissions configured for the target platform

## Notes

- Classification runs entirely on-device — works offline, no server cost, no latency from network calls
- Model accuracy is bounded by Fashion-MNIST's scope (grayscale, low-res, single-item images), so real-world photos (varied lighting, backgrounds, angles) may reduce confidence compared to the original benchmark dataset

---

*A lightweight demonstration of on-device computer vision in Flutter — from trained model to mobile inference, no cloud dependency.*
