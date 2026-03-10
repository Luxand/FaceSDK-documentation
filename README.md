# Luxand FaceSDK 8.3 — Documentation

Official developer documentation for **Luxand FaceSDK 8.3**, a cross-platform face detection and recognition library.

## What is FaceSDK?

Luxand FaceSDK provides an API to:

- **Detect and track faces** in images and live video (including thermal images)
- **Recognize faces** with high-speed template matching (53M+ matches/sec multi-threaded)
- **Detect 70 facial feature points** (eyes, eyebrows, mouth, nose, face contour)
- **Recognize gender, age, and facial expressions** (smile, open/closed eyes)
- **Liveness detection** — distinguish live subjects from photos/videos (iBeta Level 1 & 2 certified)
- **Tracker API** — assign IDs, tag names, and recognize subjects in real-time video streams

## Supported Platforms

| Platform | Architectures |
|----------|--------------|
| Windows 7/8/10/11, Server 2008R2–2022 | x86, x64 |
| Linux (glibc 2.28+) | x86_64, armv7, arm64 |
| macOS 10.13+ | arm64, x86_64 |
| iOS 12.0+ | arm64, armv7, x86_64, x86 |
| Android 5.0+ (API 21+) | arm64-v8a, armeabi-v7a, x86, x86_64 |

## Language Support

C/C++, C# .NET, VB .NET, Delphi (RAD Studio 12+), Java, Python, Swift/Objective-C (iOS), Kotlin/Java (Android), Flutter, React Native, WebAssembly.

## Documentation

The full developer guide is in [`Luxand_FaceSDK_v8_3.md`](Luxand_FaceSDK_v8_3.md) and covers:

- Getting started and library activation
- Configuration and initialization
- Working with images
- Face detection and facial feature detection
- Face matching and template management
- Gender, age, and expression recognition
- Liveness detection (including iBeta certified add-on)
- Camera integration (webcam and IP cameras)
- Tracker API for real-time video recognition
- Multi-core support and thread safety
- Migration guide and error codes

## Quick Start

1. Download FaceSDK from [luxand.com](https://www.luxand.com/facesdk/)
2. Activate the library with your license key
3. Initialize the SDK and start detecting faces

```python
import FSDK

FSDK.ActivateLibrary("your-license-key")
FSDK.Initialize()

image = FSDK.LoadImageFromFile("photo.jpg")
face = FSDK.DetectFace(image)
features = FSDK.DetectFacialFeatures(image)

FSDK.FreeImage(image)
FSDK.Finalize()
```

## System Requirements

**Minimum:** 1 GHz processor, 256 MB RAM

**Recommended:** Intel Core i7/i9/Xeon or AMD Ryzen, 2 GB RAM

## Links

- [Luxand Website](https://www.luxand.com)
- [FaceSDK Product Page](https://www.luxand.com/facesdk/)

---

Copyright 2005–2026 Luxand, Inc.
