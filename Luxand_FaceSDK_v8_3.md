<table align="center">
  <tr>
    <td align="left" valign="top">
      <img src="https://www.luxand.com/facesdk/documentation/images/luxand.png" id="image1" width="168" height="62">
    </td>
    <td align="right" valign="top">
      <div>Luxand, Inc.</div>
      <div>https://www.luxand.com</div>
    </td>
  </tr>
</table>
<br>
<div align="center">
  <h1>Luxand FaceSDK</h1>
  <h2>8.3</h2>
  <h3>Face Detection and Recognition Library</h3>
  <h3>Developer’s Guide</h3>
</div>

---

Copyright © 2005–2026 Luxand, Inc. https://www.luxand.com

<a id="overview"></a>
# Overview

Luxand FaceSDK is a cross-platform face detection and recognition library that can be easily integrated into the customer's application. FaceSDK offers the API (Application Programming Interface) to detect and track faces and facial features, to recognize gender, age and facial expressions (if a smile is present and if the eyes are open or closed), and to recognize faces on still images and videos. FaceSDK also allows detecting faces on thermal images.

FaceSDK is provided with Tracker API which allows tracking and recognizing faces in live video. Tracker API simplifies working with video streams, offering the functions to tag subjects with names and recognize them further.

The SDK provides the coordinates of [70 facial feature points](#detected-facial-features) (including eyes, eyebrows, mouth, nose and face contours). Luxand FaceSDK uses multiple processor cores to speed up recognition. The library supports MediaFoundation and DirectShow-compatible web cameras on Windows, v4l2-compatible web cameras on Linux and IP cameras with an HTTP/MJPEG interface on every platform.

Luxand FaceSDK is a dynamic link library available for 32-bit and 64-bit versions of Windows and Linux, 64-bit macOS (arm64, x86_64), iOS, Android. The SDK contains interface header files and sample applications for C++, Microsoft Visual C++ 2010+, Visual Basic .NET 2010+, Microsoft C# .NET 2010+, Embracadero RAD Studio 12+, Netbeans (Java), Xcode 7+ (iOS), Android Studio (Android), Python, Flutter and React Native.

<a id="requirements"></a>
# Requirements

The FaceSDK library supports the following platforms:

- Windows 2008R2/2012/2016/2019/2022, Windows 7, Windows 8, Windows 10, Windows 11
- Linux (RHEL 8+, CentOS 8+ and other with glibc 2.28+)
- Linux armv7/arm64 (Raspberry Pi2+)
- macOS 10.13+, arm64/x86_64
- iOS 12.0+, arm64/ armv7/ x86_64/ x86(iPhone, iPad, simulator)
- Android 5.0+ (platform version 21+), arm64 (arm64-v8a)/ armv7 (armeabi-v7a)/ x86/ x86_64

An Intel Xeon or AMD Ryzen processor is recommended for better performance.

Minimum system requirements:

- 1 GHz processor
- 256 MB RAM

Recommended system requirements:

- Intel Core i7, i9, Xeon or AMD Ryzen processor
- 2 GB RAM
- MediaFoundation/DirectShow/v4l2-compatible webcam (on Windows or Linux)
- IP camera with MJPEG interface (like AXIS IP cameras)

Note that the web camera functions are available only on Windows and Linux. IP cameras are accessible on all platforms.

<a id="technical-specifications"></a>
# Technical Specifications

The FaceSDK library has the following technical specifications:

<a id="face-detection"></a>
## Face Detection

- Robust frontal face detection
- Detection of multiple faces in a photo
- Detection of faces on thermal images
- Head rotation support: -30..30 degrees of in-plane rotation and -30..30 degrees out-of-plane rotation
- Determines in-plane face rotation angle
- Detection speed:
  - Realtime detection (webcam resolution, -15..15 degrees of in-plane head rotation): 0.00154 seconds (649 FPS) (AMD*), 0.00863 seconds (116 FPS) (iOS*), 0.01414 seconds (71 FPS) (Android*)
  - Reliable detection (digital camera resolution, -30..30 degrees of in-plane head rotation): 0.0081 seconds (AMD), 0.05 seconds (iOS), 0.082 seconds (Android)
- Returned information for each detected face: (x,y) coordinates of face center, face width and rotation angle
- Easy configuration of face detection parameters

<a id="face-matching"></a>
## Face Matching

- Matching of two faces at given FAR (False Acceptance Rate) and FRR (False Rejection Rate)
- Enrollment time:
  - Webcam resolution, using FSDK_GetFaceTemplate: 0.01417 seconds (71 FPS) (AMD), 0.03725 seconds (27 FPS) (iOS), 0.0777 seconds (13 FPS) (Android)
- Template Size: 1040 bytes
- Matching speed:
  - Single thread, templates per second: 5000000 (AMD), 3205128 (iOS), 242600 (Android)
  - Multiple parallel threads, templates per second: 53763440 (AMD), 10101010 (iOS), 1096791 (Android)
- Returned information: facial similarity level
- [ROC Diagram](https://www.luxand.com/facesdk/tech/FaceSDK_8_ROC1.png)

<a id="live-video-recognition-with-tracker-api"></a>
## Live Video Recognition with Tracker API

- Assigns a unique ID to each subject detected in video
- Allows tagging any subject in video with a name, and recognizing it further
- No requirement for a subject to pose to be enrolled
- Constant learning of subjects' appearance
- Provides with estimates of false acceptance rate and recognition rate
- Tracks multiple faces and their facial features
- Recognizes male and female genders
- Recognizes age
- Recognizes facial expressions
- Detects whether a subject is live

<a id="facial-feature-detection"></a>
## Facial Feature Detection

- Detection of 70 facial feature points (eyes, eyebrows, mouth, nose, face contour)
- Detection time (using FSDK_DetectFacialFeaturesInRegion, not including face detection stage): 0.00027 seconds (3733 FPS) (AMD), 0.0003 seconds (3333 FPS) (iOS), 0.00188 seconds (531 FPS) (Android)
- Allowed head rotation: -30..30 degrees of in-plane rotation, -20..20 degrees out-of-plane rotation
- Returned information: array of 70 (x,y) coordinates of each facial feature point

<a id="eye-centers-detection"></a>
## Eye Centers Detection

- Detection of eye centers only, detection time (not including face detection stage): 0.00027 seconds (3752 FPS) (AMD), 0.00028 seconds (3571 FPS) (iOS), 0.00188 seconds (531 FPS) (Android)
- Returned information: two (x,y) coordinates of left eye center and right eye center

<a id="gender-recognition"></a>
## Gender Recognition

- Recognition of different genders
- Gender recognition time (not including face and facial feature detection stages): 0.0039 seconds (AMD), 0.0063 seconds (iOS), 0.0122 seconds (Android)
- Returned information: confidence level in each gender

<a id="age-recognition"></a>
## Age Recognition

- Recognition of age
- Age recognition time (not including face and facial feature detection stages): 0.0051 seconds (AMD), 0.0075 seconds (iOS), 0.0131 seconds (Android)
- Returned information: age of a person
- Depending on source quality and lighting conditions, error rate is +/- 5 years

<a id="facial-expression-recognition"></a>
## Facial Expression Recognition

- Recognizes if the subject smiles and if the eyes are open or closed
- Expression recognition time (not including face and facial feature detection stages): 0.0043 seconds (AMD), 0.0063 seconds (iOS), 0.0122 seconds (Android)
- Returned information: confidence level in each facial expression

<a id="liveness-detection"></a>
## Liveness detection

- Detects whether the subject is live (i.e. not a photo/video presented to the camera)
- Works with still images and videos
- Liveness detection time (not including face and facial feature detection stages): 0.017 seconds (AMD), 0.016 seconds (iOS), 0.034 seconds (Android)
- Returned information: the probability of the subject being live

<a id="multi-core-support"></a>
## Multi-Core Support

- The library supports using multiple processes when executing face detection or recognition functions to maximize the performance.

<a id="library-size"></a>
## Library Size

- The size of the redistributables does not exceed 160 MB for each platform.

---

**Performance Benchmarks:**

*Measured on AMD Ryzen 5 1600X processor with 12 threads, iPhone X with 6 threads, Google Pixel 2 (Snapdragon 835) with 8 threads.*

<a id="distribution"></a>
# Distribution

Please download the latest version of Luxand FaceSDK from: [https://www.luxand.com/facesdk/download/](https://www.luxand.com/facesdk/download/)

<a id="binaries-directory-structure"></a>
## Binaries Directory Structure

The FaceSDK binaries directory contains the following directories and files:

| Directory | Description |
|-----------|-------------|
| **Binaries\Android** | FaceSDK Android binaries (armeabi-v7a, arm64-v8a, x86, x86_64) |
| **Binaries\iOS** | FaceSDK iOS binaries (static and shared) |
| **Binaries\Linux** | FaceSDK Linux binaries (aarch64, armv7, x86, x86_64) |
| **Binaries\macOS** | FaceSDK macOS (x86_64, arm64) |
| **Binaries\Windows** | FaceSDK Windows binaries (win32, x64) |

<a id="wrappers"></a>
## Wrappers

The wrappers directory contains the following:

| Directory | Description |
|-----------|-------------|
| **Wrappers\dotNet** | .Net wrapper (including FaceSDK.NET.dll) |
| **Wrappers\Android** | Android wrapper (FSDK.java) |
| **Wrappers\C** | LuxandFaceSDK.h - include file for C/C++. |
| **Wrappers\Delphi** | Delphi wrapper (LuxandFaceSDK.pas) |
| **Wrappers\Java** | Java wrapper (NetBeans, including FaceSDK.jar and jna.jar) |
| **Wrappers\Python** | Python wrapper |
| **Wrappers\WebAssembly** | WASM wrapper (including simd support) |

<a id="demo"></a>
## Demo

The demo directory contains the following applications:

| Application | Description |
|-------------|-------------|
| **FaceSDKWelcome** | A welcome application that you can use to launch other demo applications, get a hardware ID, or click on a link to documentation and order. |
| **FacialFeatureDemo** | A demo application for displaying facial features. |
| **LiveRecognitionDemo** | A demo application that recognizes faces and shows age, gender, and facial expression. |
| **Panorama** | A demo application that shows several panoramic images, determines the angles of the face and rotates the image. |
| **PhotoDemo** | A demo application that receives a picture, detects a face and facial features, and, if the face is found, crops it. |

<a id="sample-applications"></a>
# Sample Applications

FaceSDK is distributed with the following sample applications:

<a id="1-live-recognition"></a>
## 1. Live Recognition

This application receives video from a camera, allows tagging any subject with a name, and then display the name (recognizing the subject). The application utilizes Tracker API. The iOS/Android versions are published in the Apple AppStore and in Google Play ("Luxand Face Recognition" application).

**Try online:** [Live Recognition](https://www.luxand.com/download/wasm/LiveRecognition.html)

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/LiveRecognition-VisualStudio-CSharp.zip)
- [iOS (Objective-C)](https://www.luxand.com/download/samples/LiveRecognition-iOS-ObjectiveC.zip)
- [iOS (Swift)](https://www.luxand.com/download/samples/LiveRecognition-iOS-Swift.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/LiveRecognition-Android.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/LiveRecognition-Delphi.zip)
- [C++/GTK 3.0+ (CMake 3.20+)](https://www.luxand.com/download/samples/LiveRecognition-CPP-GTK.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/LiveRecognition-VisualStudio-CPP.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/LiveRecognition-VisualStudio-VBNet.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/LiveRecognition-Java-NetBeans.zip)
- [WebAssembly (Wasm)](https://www.luxand.com/download/samples/LiveRecognition-WebAssembly.zip)

<a id="2-face-tracking"></a>
## 2. Face Tracking

This application receives video from a webcam and highlights all detected faces with rectangles. The application utilizes Tracker API.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/FaceTracking-VisualStudio-CSharp.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/FaceTracking-Delphi.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/FaceTracking-VisualStudio-CPP.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/FaceTracking-VisualStudio-VBNet.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/FaceTracking-Java-NetBeans.zip)

<a id="3-lookalikes"></a>
## 3. Lookalikes

This application allows the user to create a database of faces and run a search for the best matches (the most similar face from the database is shown). To run the Microsoft SQL example, you need to attach the database (located in the DB folder of the sample) to the Microsoft SQL Server.

**Source code is available on:**
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/Lookalikes-VisualStudio-CPP.zip)
- [Microsoft Visual C++ 2017+ (with SQLite)](https://www.luxand.com/download/samples/Lookalikes-VisualStudio-CPP-SQLite.zip)
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/Lookalikes-VisualStudio-CSharp.zip)
- [Microsoft C# 2010+ (with MS SQL)](https://www.luxand.com/download/samples/Lookalikes-VisualStudio-CSharp-MSSQL.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/Lookalikes-Java-NetBeans.zip)

<a id="4-live-facial-features"></a>
## 4. Live Facial Features

This application tracks users' facial features in real time using a web camera. The coordinates of facial features are smoothed by Tracker API to prevent jitter.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/LiveFacialFeatures-VisualStudio-CSharp.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/LiveFacialFeatures-Delphi.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/LiveFacialFeatures-Java-NetBeans.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/LiveFacialFeatures-VisualStudio-CPP.zip)
- [iOS (Objective-C)](https://www.luxand.com/download/samples/LiveFacialFeatures-iOS-ObjectiveC.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/LiveFacialFeatures-Android.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/LiveFacialFeatures-VisualStudio-VBNet.zip)
- [WebAssembly (Wasm)](https://www.luxand.com/download/samples/LiveFacialFeatures-WebAssembly.zip)

<a id="5-age-gender-expression"></a>
## 5. Age Gender Expression

Using Tracker API, this application recognizes the gender, age, and facial expression (smile, eyes open/closed) of a subject looking into a webcam.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/AgeGenderExpression-VisualStudio-CSharp.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/AgeGenderExpression-Delphi.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/AgeGenderExpression-Java-NetBeans.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/AgeGenderExpression-VisualStudio-CPP.zip)
- [iOS (Swift)](https://www.luxand.com/download/samples/AgeGenderExpression-iOS-Swift.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/AgeGenderExpression-Android.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/AgeGenderExpression-VisualStudio-VBNet.zip)

<a id="6-facial-features"></a>
## 6. Facial Features

This application opens a photo, detects a face in a photo (only one face, the one that can be detected best), detects facial features and draws a frame around the detected face and detected features.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/FacialFeatures-VisualStudio-CSharp.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/FacialFeatures-Delphi.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/FacialFeatures-Java-NetBeans.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/FacialFeatures-VisualStudio-CPP.zip)
- [iOS (Objective-C)](https://www.luxand.com/download/samples/FacialFeatures-iOS-ObjectiveC.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/FacialFeatures-Android.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/FacialFeatures-VisualStudio-VBNet.zip)
- [WebAssembly (Wasm)](https://www.luxand.com/download/samples/FacialFeatures-WebAssembly.zip)

<a id="7-ip-camera"></a>
## 7. IP Camera

This application opens an IP camera (allowing the user to specify its address, user name and password), displays the image from the camera and tracks faces. The application utilizes Tracker API.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/IPCamera-VisualStudio-CSharp.zip)
- [Embracadero RAD Studio 12+](https://www.luxand.com/download/samples/IPCamera-Delphi.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/IPCamera-Java-NetBeans.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/IPCamera-VisualStudio-CPP.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/IPCamera-VisualStudio-VBNet.zip)

<a id="8-portrait"></a>
## 8. Portrait

This application is for the command line. The application receives a picture, detects a face and, if the face is found, crops it and saves it to a file.

**Source code is available on:**
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/Portrait-VisualStudio-CPP.zip)

<a id="9-thermal"></a>
## 9. Thermal

This application loads a thermal face detection model and allows you to open a grayscale thermal image (which you may have received from a thermal camera), detect faces on the image and draw frames around the detected faces.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/Thermal-VisualStudio-CSharp.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/Thermal-VisualStudio-CPP.zip)
- [iOS (Objective-C)](https://www.luxand.com/download/samples/Thermal-iOS-ObjectiveC.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/Thermal-Android.zip)

<a id="10-active-liveness"></a>
## 10. Active Liveness

This application asks a subject looking into a camera to rotate their head and smile in a certain way to detect liveness. The active liveness detection helps prevent spoofing attacks with photos or videos by requiring user interaction.

**Try online:** [Active Liveness](https://www.luxand.com/download/wasm/ActiveLiveness.html)

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/ActiveLiveness-VisualStudio-CSharp.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/ActiveLiveness-VisualStudio-CPP.zip)
- [iOS (Swift)](https://www.luxand.com/download/samples/ActiveLiveness-iOS-Swift.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/ActiveLiveness-Android.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/ActiveLiveness-Java-NetBeans.zip)
- [WebAssembly (Wasm)](https://www.luxand.com/download/samples/ActiveLiveness-WebAssembly.zip)

<a id="11-passive-liveness"></a>
## 11. Passive Liveness

This application automatically detects the liveness of a subject looking into a camera (without any assistance from the subject). Uses AI-based analysis to detect spoofing attempts without requiring user actions.

**Source code is available on:**
- [Microsoft C# 2010+](https://www.luxand.com/download/samples/PassiveLiveness-VisualStudio-CSharp.zip)
- [Microsoft Visual C++ 2017+](https://www.luxand.com/download/samples/PassiveLiveness-VisualStudio-CPP.zip)
- [iOS (Swift)](https://www.luxand.com/download/samples/PassiveLiveness-iOS-Swift.zip)
- [Android (Android Studio)](https://www.luxand.com/download/samples/PassiveLiveness-Android.zip)
- [Java (NetBeans)](https://www.luxand.com/download/samples/PassiveLiveness-Java-NetBeans.zip)
- [Microsoft Visual Basic .NET 2010+](https://www.luxand.com/download/samples/PassiveLiveness-VisualStudio-VBNet.zip)

<a id="12-ibeta-liveness"></a>
## 12. IBeta Liveness

This sample demonstrates IBeta-compliant liveness detection that analyzes faces to determine if they are real or presentation attacks (photo, video, mask, etc.). The sample includes desktop implementations for Windows and Linux, mobile implementations for iOS and Android, and advanced implementations supporting Flutter, React Native, and Python.

**Desktop:**
- [Windows (C++)](https://www.luxand.com/download/samples/iBeta_Liveness-Windows-CPP.zip)
- [Windows (C#)](https://www.luxand.com/download/samples/iBeta_Liveness-Windows-CSharp.zip)
- [Windows (C# WinUI)](https://www.luxand.com/download/samples/iBeta_Liveness-Windows-CSharp-WinUI.zip)
- [Linux (C++)](https://www.luxand.com/download/samples/iBeta_Liveness-Linux-CPP.zip)

**Mobile:**
- [iOS (Swift)](https://www.luxand.com/download/samples/iBeta_Liveness-iOS-Swift.zip)
- [Android (Java)](https://www.luxand.com/download/samples/iBeta_Liveness-Android-Java.zip)

**Advanced:**
- [Python (Windows)](https://www.luxand.com/download/samples/iBeta_Liveness-Python_Windows.zip)
- [Python (Linux)](https://www.luxand.com/download/samples/iBeta_Liveness-Python_Linux.zip)
- [Flutter (iOS, Android)](https://www.luxand.com/download/samples/iBeta_Liveness-Flutter.zip)
- [React Native (iOS, Android)](https://www.luxand.com/download/samples/iBeta_Liveness-ReactNative.zip)

<a id="13-advanced---python"></a>
## 13. Advanced - Python

This sample provides comprehensive Python implementations demonstrating various FaceSDK capabilities. The sample includes multiple Python scripts for active liveness, passive liveness, facial features detection, live recognition, lookalikes search, portrait cropping, thermal image processing, and tracker memory management. The Python wrapper allows dynamic linking with .dll/.so/.dylib and provides cross-platform support for Windows, Linux (x86, ARM), and macOS.

**Source code is available on:**
- [Python 3.x (Windows)](https://www.luxand.com/download/samples/Advanced-Python-Windows.zip)
- [Python 3.x (Linux)](https://www.luxand.com/download/samples/Advanced-Python-Linux.zip)

**Included Python scripts:**
- `ActiveLiveness.py` - Active liveness detection with user interaction.
- `PassiveLiveness.py` - Automatic passive liveness detection.
- `FacialFeatures.py` - Facial feature detection in static images (Windows only, uses GDI+).
- `LiveFacialFeatures.py` - Real-time facial features from camera (Windows only).
- `LiveFacialFeatures_tk.py` - Cross-platform real-time facial features using Tkinter.
- `LiveRecognition.py` - Real-time face recognition from camera (Windows only).
- `LiveRecognition_tk.py` - Cross-platform face recognition using Tkinter.
- `Lookalikes.py` - Find similar faces in a database.
- `Portrait.py` - Command-line face detection and cropping.
- `Thermal.py` - Thermal image face detection.
- `trackerMemoryTool.py` - Tracker memory management utility.

<a id="14-advanced---flutter-and-react-native"></a>
## 14. Advanced - Flutter and React Native

These samples provide multi-platform implementations for Flutter and React Native, matching the LiveRecognition capabilities for face tracking and recognition.

**Source code is available on:**
- [Flutter (iOS, Android)](https://www.luxand.com/download/samples/Advanced-Flutter.zip)
- [React Native (iOS, Android)](https://www.luxand.com/download/samples/Advanced-ReactNative.zip)

<a id="using-facesdk-with-programming-languages"></a>
# Using FaceSDK with Programming Languages

To access the FaceSDK library functions, you need to use its binary file in your applications. The specific file depends on the platform:

- Windows applications use `facesdk.dll`
- Linux and Android applications use `libfsdk.so`
- macOS applications use `libfsdk.dylib`
- .NET applications use `facesdk.NET.dll` and the appropriate binary file (`facesdk.dll`, `libfsdk.dylib` or `libfsdk.so`)
- Java applications use `facesdk.jar`, `jna.jar` and the appropriate binary file (`facesdk.dll`, `libfsdk.dylib` or `libfsdk.so`)
- iOS applications use `libfsdk-static.a` or `fsdk.framework`

On Windows, Linux and macOS it is usually recommended to store this file in the directory where the executable file of your application is located. Alternatively, you may keep the file in:

- the working directory of your application
- the directory specified in the path environment variable of your system: `PATH` (Windows), `LD_LIBRARY_PATH` (Linux), `DYLD_LIBRARY_PATH` (macOS).

You need to include interface header files into your application project in order to use FaceSDK.

<a id="using-with-net-c-and-vb"></a>
# Using with .NET (C# and VB)

You need to have .NET Framework 4.8+ on your system.

For Microsoft .NET applications, you need to add the .NET component into your project.

Follow these steps to add the component in Visual Studio 2010+:

- Select Project - Add Reference - Browse
- Choose the file `Wrappers\dotNET\bin\FaceSDK.NET.dll`
- Add the following statement to the beginning of your application:

```csharp
using Luxand
```

After that you may use the methods of the `Luxand.FSDK` namespace for general FaceSDK functions, and `Luxand.Camera` class for webcam-related functions. You may refer just to `FSDK` namespace if `using Luxand` is specified.

Once `FaceSDK.NET.dll` is added to the references, it will be redistributed automatically with your application, so no specific deployment actions are required. However you need to redistribute `facesdk.dll` (or `libfsdk.so` on Linux / `libfsdk.dylib` on macOS) with your application.

By default, the documentation refers to C/C++ declarations of FaceSDK functions. For example, the function to detect a face is referred to as FSDK_DetectFace function. To refer to this function in .NET, replace the `FSDK_` prefix with `FSDK.` namespace. Thus, the reference to this function becomes `FSDK.DetectFace` (note that webcam-specific functions are located in the `Luxand.Camera` class; refer to [Working with Web Cameras](#working-with-cameras) for details).

If you are using an older version of .NET (for example, 2.0, 3.0 or 3.5) or just need a component for a specific .NET version, you may use the source code available in the `Wrappers\dotNET` directory.

<a id="using-cimage-class-in-net"></a>
# Using CImage class in .NET

CImage is a class for Microsoft .NET for easy manipulation of images. CImage encapsulates an HImage handle and provides convenient methods for applying FaceSDK functions to that image.

To start working with CImage, just create an instance of it. You can pass a file path, HImage handle, HBITMAP handle or System.Drawing.Image object to the constructor to load the corresponding object into the image. Alternatively, call the constructor without parameters to create an empty image. Refer to the functions [FSDK_LoadImageFromFile](#fsdk_loadimagefromfile-function), [FSDK_LoadImageFromHBitmap](#fsdk_loadimagefromhbitmap-function), [FSDK.LoadImageFromCLRImage](#fsdkloadimagefromclrimage-function) and [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) for further details.

A CImage instance has three properties: ImageHandle, Width and Height. ImageHandle is a handle of the internal representation of the image encapsulated by the class. Width and Height properties are the width and height of an image in pixels (see [FSDK_GetImageWidth](#fsdk_getimagewidth-function) and [FSDK_GetImageHeight](#fsdk_getimageheight-function)). If you alter the ImageHandle handle directly (for example, executing an FSDK. method applied to that image handle), you must update the CImage object by calling the [CImage.ReloadFromHandle()](#cimagereloadfromhandle) method. CImage throws an exception if any FaceSDK function, called within the CImage method, has returned an error.

Most CImage methods operating with an image (for example, the Resize() method) return the processed image as the result.

The CImage destructor releases ImageHandle, so there is no need to call FSDK.FreeImage explicitly after the instance has been destroyed.

Note that when you pass an existing image handle to the constructor, it will be freed after the destruction of the CImage class instance, and become invalid. If you need the original image handle to be valid after the CImage class instance is destroyed, consider creating a copy of the image handle and passing the copy to the CImage constructor.

---

<a id="cimage"></a>
## CImage()

Creates an empty CImage instance.

**Syntax:**

```csharp
Luxand.CImage();
```

---

<a id="cimageint"></a>
## CImage(Int)

Creates a CImage instance from image already loaded to FaceSDK.

**Syntax:**

```csharp
Luxand.CImage(int ImageHandle);
```

**Parameters:**

*ImageHandle* - the internal handle of an image already loaded to FaceSDK. The destructor will free the ImageHandle handle.

---

<a id="cimagereloadfromhandle"></a>
## CImage.ReloadFromHandle()

Updates the internal properties of a CImage instance in accordance with the ImageHandle.

**Syntax:**

```csharp
Luxand.CImage.ReloadFromHandle();
```

<a id="using-with-cc"></a>
# Using with C/C++

For Microsoft Visual C++ applications, you need to include the header file `Wrappers\C\LuxandFaceSDK.h`, and the stub library file `facesdk.lib` into your project.

<a id="installation-steps"></a>
## Installation Steps

Follow these steps to add the library to your project:

1. Copy `Wrappers\C\LuxandFaceSDK.h` into the directory of your project

2. For 32-bit applications, copy `Binaries\Windows\x86\facesdk.dll` and `Binaries\Windows\x86\facesdk.lib` into the output directory of your project

3. For 64-bit applications, copy `Binaries\Windows\x64\facesdk.dll` and `Binaries\Windows\x64\facesdk.lib` into the output directory of your project

4. Choose Project Properties - Linker - Input - Additional Dependencies, and add `facesdk.lib` string

5. Choose Project Properties - Linker - General - Additional Library Directories Dependencies, and add `$(OutDir)` string (a reference to the output directory)

6. Add the following statement to the beginning of your application:

```cpp
#include "LuxandFaceSDK.h"
```

<a id="output-directory"></a>
## Output Directory

The output directory `$(OutDir)` typically refers to `Debug\` or `Release\` in the directory of your solution. You may change it in the Configuration Properties - General of your project. You may also choose another directory to store the .lib file, but it is recommended to keep `facesdk.dll` in the directory where the executable file of your application is located.

<a id="redistribution"></a>
## Redistribution

You need to redistribute the file `facesdk.dll` with your application.

<a id="using-with-delphi"></a>
# Using with Delphi

For Delphi applications, put `facesdk.dll` into the working directory of your application and use the `Wrappers\Delphi\LuxandFaceSDK.pas` unit in your project.

You need to redistribute the file `facesdk.dll` with your application.

<a id="using-with-java"></a>
# Using with Java

You need JDK 1.6 (or OpenJDK 1.6) to use FaceSDK with Java. The FaceSDK Java wrapper uses JNA (all information about JNA and the actual version can be found at https://github.com/twall/jna, but jna.jar is included in the distribution for your convenience). The FaceSDK java wrapper works with any IDE, but only Netbeans sample projects are provided with the distribution.

<a id="setup-in-netbeans"></a>
## Setup in NetBeans

To use FaceSDK in your Netbeans project, follow these steps:

1) Add FaceSDK.jar (`Wrappers\Java\FaceSDK.jar`) and jna.jar (`Wrappers\Java\jna.jar`) to the Libraries section of the project.

2) Add the following imports to your source code:

```java
import Luxand.*;
import Luxand.FSDK.*;
import Luxand.FSDKCam.*;
```

3) Put the appropriate facesdk binaries (`facesdk.dll`, `libfdsk.so` or `libfdsk.dylib`) in the project directory (or to the `/usr/lib` directory if using OpenJDK).

<a id="distribution"></a>
## Distribution

You need to redistribute the FaceSDK binaries (`facesdk.dll`, `libfdsk.so` or `libfdsk.dylib`) as well as `FaceSDK.jar` and `jna.jar` with your application.

<a id="using-with-cocoa"></a>
# Using with Cocoa

If you are using Cocoa to write an application in Xcode, make sure that your source code files (which use FaceSDK) have the `.mm` extension, so they are compiled as Objective-C++. If the files have the `.m` extension, they are compiled as Objective-C and cannot use FaceSDK.

<a id="using-with-ios"></a>
# Using with iOS

Refer to the [Using with Cocoa](#using-with-cocoa) section. In Objective-C you should use the C++ syntax within your program.

To enable FaceSDK support in your Xcode iOS project, add `Binaries/iOS/static/libfsdk-static.a` and `Wrappers/C/LuxandFaceSDK.h` to your project.

<a id="using-with-android"></a>
# Using with Android

For Android Studio you need to copy the directories armeabi-v7a and arm64-v8a contained in `Binaries/android/` to the `app/src/main/jniLibs` directory of your project. You also need to add the `Wrappers/android/FSDK.java` file to the `app/src/main/java/com/luxand` directory.

The syntax of some functions on Android is different from the corresponding Java syntax due to the usage of JNI instead of JNA.

**Note:** Only arm64 (arm64-v8a), armv7 (armeabi-v7a), x86 and x86_64 architectures are supported by FaceSDK on the Android platform.

The FSDK class is provided in the binary code form only. Therefore, the "com.luxand" package name of this class cannot be changed.

<a id="using-with-python"></a>
# Using with Python

To use FaceSDK, you must have Python 2.7 or later installed.

Copy the Python wrapper to your working directory, or place it in the python/lib/fsdk directory.

For Windows users: If using a global path folder, also copy win.py to the same wrapper directory.

To start working with FaceSDK add the import:

```python
from fsdk import FSDK
```

Unlike other wrappers, all functions in the Python wrapper never return error code of execution, instead the result of function is returned or None. In case of an error a corresponding exception is raised.

<a id="sample-code"></a>
## Sample Code

Try python samples at:
- Windows: https://www.luxand.com/download/samples/Advanced-Python-Windows.zip
- Linux: https://www.luxand.com/download/samples/Advanced-Python-Linux.zip

<a id="using-with-flutter"></a>
# Using with Flutter

Please refer to the sample at [https://www.luxand.com/download/samples/Advanced-Flutter.zip](https://www.luxand.com/download/samples/Advanced-Flutter.zip) and follow the instructions in the readme.md file within that directory.

<a id="using-with-react-native"></a>
# Using with React Native

Please refer to the sample at [https://www.luxand.com/download/samples/Advanced-ReactNative.zip](https://www.luxand.com/download/samples/Advanced-ReactNative.zip) and follow the instructions in the readme.md file within that directory.

<a id="using-with-web-assembly"></a>
# Using with Web Assembly

Please refer to the samples at:

- [https://www.luxand.com/download/samples/ActiveLiveness-WebAssembly.zip](https://www.luxand.com/download/samples/ActiveLiveness-WebAssembly.zip)
- [https://www.luxand.com/download/samples/LiveRecognition-WebAssembly.zip](https://www.luxand.com/download/samples/LiveRecognition-WebAssembly.zip)
- [https://www.luxand.com/download/samples/LiveFacialFeatures-WebAssembly.zip](https://www.luxand.com/download/samples/LiveFacialFeatures-WebAssembly.zip)

<a id="unicode-support"></a>
# Unicode Support

The library supports Unicode filenames on the Windows platform. If you work with file names in the Unicode character set, use functions [FSDK_LoadImageFromFileW](#fsdk_loadimagefromfilew-function) and [FSDK_SaveImageToFileW](#fsdk_saveimagetofilew-function) to open and save files.

<a id="redistributables"></a>
# Redistributables

The following files may be redistributed with your application:

| Platform | Files |
|----------|-------|
| Windows | `Binaries\Windows\x86\facesdk.dll` (for 32-bit systems)<br>`Binaries\Windows\x64\facesdk.dll` (for 64-bit systems) |
| Linux | `Binaries\Linux\x86\libfsdk.so` (for 32-bit systems)<br>`Binaries\Linux\x86_64\libfsdk.so` (for 64-bit systems)<br>`Binaries\Linux\armv7\libfsdk.so` (for armv7 systems)<br>`Binaries\Linux\aarch64\libfsdk.so` (for arm64 systems) |
| macOS | `Binaries\macOS\x86_64\libfsdk.dylib`<br>`Binaries\macOS\arm64\libfsdk.dylib` |
| Android | `Binaries\Android\arm64-v8a\libfsdk.so`<br>`Binaries\Android\armeabi-v7a\libfsdk.so`<br>`Binaries\Android\x86\libfsdk.so`<br>`Binaries\Android\x86_64\libfsdk.so` |
| iOS | `Binaries\iOS\shared\fsdk.framework` |
| .NET | `Wrappers\dotNet\bin\FaceSDK.NET.dll` |
| Java (on Windows / Linux / macOS) | `Wrappers\Java\FaceSDK.jar`<br>`Wrappers\Java\jna.jar` |
| Thermal face detection | `thermal.bin` (the detection model used in Thermal samples) |

<a id="usage-scenarios"></a>
# Usage Scenarios

The library usage level depends on the functionality required from Luxand FaceSDK.

If you work with video, consider using Tracker API, as the API provides high-level functions to recognize subjects and tag them with names, to track their faces and facial features, and to recognize gender, age and facial expressions. The usage scenario for Tracker API can be found in the Usage Scenario section of the [Tracker API](#tracker-api-face-recognition-and-tracking-in-video-streams) chapter.

Otherwise, the typical scenario is as follows:

1. Activate FaceSDK by calling up the [FSDK_ActivateLibrary](#fsdk_activatelibrary-function) function with the key sent by Luxand, Inc.

2. Initialize FaceSDK by calling up the [FSDK_Initialize](#fsdk_initialize-function) function.

3. Load images either from file, buffer, or the HBITMAP handle ([FSDK_LoadImageFromFile](#fsdk_loadimagefromfile-function), [FSDK_LoadImageFromBuffer](#fsdk_loadimagefrombuffer-function), [FSDK_LoadImageFromHBitmap](#fsdk_loadimagefromhbitmap-function) functions).

4. Set face detection parameters if needed ([FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function), [FSDK_SetFaceDetectionThreshold](#fsdk_setfacedetectionthreshold-function)).

5. Use FaceSDK functions:
   - Detect a face ([FSDK_DetectFace](#fsdk_detectface-function)) or multiple faces ([FSDK_DetectMultipleFaces](#fsdk_detectmultiplefaces-function)) in an image
   - Detect facial features if needed ([FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function), [FSDK_DetectFacialFeaturesInRegion](#fsdk_detectfacialfeaturesinregion-function))
   - Extract a face template from the image ([FSDK_GetFaceTemplate](#fsdk_getfacetemplate-function), [FSDK_GetFaceTemplateInRegion](#fsdk_getfacetemplateinregion-function), [FSDK_GetFaceTemplateUsingFeatures](#fsdk_getfacetemplateusingfeatures-function))
   - Match face templates ([FSDK_MatchFaces](#fsdk_matchfaces-function)) and acquire facial similarity level
   - To find out if a face belongs to the same person, calculate the matching threshold at a given FAR or FRR rate ([FSDK_GetMatchingThresholdAtFAR](#fsdk_getmatchingthresholdatfar-function) and [FSDK_GetMatchingThresholdAtFRR](#fsdk_getmatchingthresholdatfrr-function) functions).

6. Finalize the FaceSDK library ([FSDK_Finalize](#fsdk_finalize-function) function).

<a id="working-with-a-camera"></a>
## Working with a Camera

To work with a camera, follow these steps*:

1. Initialize camera capturing ([FSDK_InitializeCapturing](#fsdk_initializecapturing-function)).

2. Get a list of web cameras available in the system ([FSDK_GetCameraList](#fsdk_getcameralist-function)).

3. Get list of video formats supported by the camera ([FSDK_GetVideoFormatList](#fsdk_getvideoformatlist-function)).

4. Set the desired video format for the chosen camera ([FSDK_SetVideoFormat](#fsdk_setvideoformat-function)).

5. Open a web camera ([FSDK_OpenVideoCamera](#fsdk_openvideocamera-function)) or an IP camera ([FSDK_OpenIPVideoCamera](#fsdk_openipvideocamera-function)).

6. Grab frames ([FSDK_GrabFrame](#fsdk_grabframe-function)) in a loop, displaying them and detecting/recognizing faces.

7. Close video camera ([FSDK_CloseVideoCamera](#fsdk_closevideocamera-function)).

8. Delete the list of video formats ([FSDK_FreeVideoFormatList](#fsdk_freevideoformatlist-function)).

9. Delete the list of web cameras ([FSDK_FreeCameraList](#fsdk_freecameralist-function)).

10. Finalize capturing ([FSDK_FinalizeCapturing](#fsdk_finalizecapturing-function)).

*If you work with an IP camera, you should not follow steps 2, 3, 4, 8 and 9.

<a id="library-activation"></a>
# Library Activation

FaceSDK is a copy-protected library, and must be activated with a license key before its use. You need to pass the license key received from Luxand, Inc. to the [FSDK_ActivateLibrary](#fsdk_activatelibrary-function) function before initializing Luxand FaceSDK. Almost all FaceSDK functions will return the FSDKE_NOT_ACTIVATED error code in case the library is not activated. To retrieve your license information, call [FSDK_GetLicenseInfo](#fsdk_getlicenseinfo-function). This function returns the name the library is licensed to. You may need to use the [FSDK_GetHardware_ID](#fsdk_gethardware_id-function) function to obtain your hardware ID if your license is restricted to one machine only. Additionally, you can find out hardware ID by running the hardwareid program (ShowHardwareID.exe for Windows).

You may request a temporary evaluation key from Luxand, Inc.:

https://luxand.com/facesdk/requestkey/.

<a id="fsdk_gethardware_id-function"></a>
## FSDK_GetHardware_ID Function

Generates a Hardware ID code.

**C++ Syntax:**

```cpp
int FSDK_GetHardware_ID(char* HardwareID);
```

**Delphi Syntax:**

```pascal
function FSDK_GetHardware_ID(HardwareID: PChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetHardwareID(out string HardwareID);
```

**Java Syntax:**

```java
int FSDK.GetHardware_ID(String HardwareID[]);
```

**iOS and Android: not implemented.**

**Parameters:**

*HardwareID* - address of the null-terminated string for receiving the Hardware ID code.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetHardware_ID() -> str
```

**Return Value:**

A Hardware ID code.

<a id="fsdk_activatelibrary-function"></a>
## FSDK_ActivateLibrary Function

Activates the FaceSDK library.

**C++ Syntax:**

```cpp
int FSDK_ActivateLibrary(char* LicenseKey);
```

**Delphi Syntax:**

```pascal
function FSDK_ActivateLibrary(LicenseKey: PChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.ActivateLibrary(out string LicenseKey);
```

**Java and Android Syntax:**

```java
int FSDK.ActivateLibrary(String LicenseKey);
```

**Parameters:**

*LicenseKey* - License key you received from Luxand, Inc.

**Return Value:**

Returns FSDKE_OK if the registration key is valid and not expired.

**Python Syntax:**

```python
def FSDK.ActivateLibrary(license_key: str)
```

**Return Value:**

None

**Exceptions:**

FSDK.NotActivated if key is invalid or expired.

This exception is also raised from all FSDK functions if library is not activated.

<a id="fsdk_getlicenseinfo-function"></a>
## FSDK_GetLicenseInfo Function

Retrieves license information.

**C++ Syntax:**

```cpp
int FSDK_GetLicenseInfo(char* LicenseInfo);
```

**Delphi Syntax:**

```pascal
function FSDK_GetLicenseInfo(LicenseInfo: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetLicenseInfo(out string LicenseInfo);
```

**Java and Android Syntax:**

```java
int FSDK.GetLicenseInfo(String LicenseInfo[]);
```

**Parameters:**

*LicenseInfo* - address of the null-terminated string for receiving the license information. This variable should be allocated no less than 256 bytes of memory.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetLicenseInfo() -> str
```

**Return Value:**

The license information string.

<a id="fsdk_getversioninfo-function"></a>
## FSDK_GetVersionInfo Function

Use the FSDK_GetVersionInfo function to get information about the current version of the FaceSDK library.

**C++ Syntax:**

```cpp
int FSDK_GetVersionInfo(const char** VersionInfo);
```

**Delphi Syntax:**

```pascal
type
  PPAnsiChar = ^PAnsiChar;
function FSDK_GetVersionInfo(VersionInfo: PPAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetVersionInfo(out string VersionInfo);
```

**Java and Android Syntax:**

```java
int FSDK.GetVersionInfo(String[] VersionInfo);
```

**Parameters:**

*VersionInfo* - a pointer to an address of the null-terminated string for receiving the license information.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetVersionInfo() -> str
```

**Return Value:**

The string containing information about the current version of the FaceSDK library.

<a id="initialization"></a>
# Initialization

<a id="fsdk_initialize-function"></a>
## FSDK_Initialize Function

Initializes the FaceSDK library. Should be called before using of any face detection functions.

**C++ Syntax:**

```cpp
int FSDK_Initialize(char* DataFilesPath);
```

**Delphi Syntax:**

```pascal
function FSDK_Initialize(DataFilesPath: PChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.InitializeLibrary();
```

**Java and Android Syntax:**

```java
int FSDK.Initialize();
```

**Parameters:**

*DataFilesPath* - pointer to the null-terminated string specifying the path where facesdk.dll is stored. An empty string means the current directory. (Note: the parameter is not used since version 1.8; an empty string might be passed as this parameter.)

**Return Value:**

Returns FSDKE_OK if successful or FSDK_IO_ERROR if an I/O error occurs.

**Python Syntax:**

```python
def FSDK.Initialize(dataFilesPath='');
```

**Return Value:**

None

<a id="fsdk_finalize-function"></a>
## FSDK_Finalize Function

Finalizes the FaceSDK library. Should be called when the application is exited. Before calling FSDK_Finalize, you must release all FaceSDK resources in the correct order to avoid memory leaks or undefined behavior.

**C++ Syntax:**

```cpp
int FSDK_Finalize();
```

**Delphi Syntax:**

```pascal
function FSDK_Finalize: integer;
```

**C# Syntax:**

```csharp
int FSDK.FinalizeLibrary();
```

**Java and Android Syntax:**

```java
int FSDK.Finalize();
```

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.Finalize();
```

**Return Value:**

None

<a id="resource-cleanup-guide"></a>
# Resource Cleanup Guide

When your application finishes using FaceSDK, all resources should be released.

<a id="cleanup-order"></a>
## Cleanup Order

Typically, the cleanup sequence is as follows:

1. **Save tracker memory** (if needed) — call [FSDK_SaveTrackerMemoryToFile](#fsdk_savetrackermemorytofile-function) or [FSDK_SaveTrackerMemoryToBuffer](#fsdk_savetrackermemorytobuffer-function)
2. **Free tracker handles** — call [FSDK_FreeTracker](#fsdk_freetracker-function) for each created tracker
3. **Close video cameras** — call [FSDK_CloseVideoCamera](#fsdk_closevideocamera-function) for each open camera

<a id="cleanup-example-c"></a>
## Cleanup Example (C++)

```cpp
// Proper cleanup sequence with error handling
// Step 1: Save tracker memory if needed
int err = FSDK_SaveTrackerMemoryToFile(tracker, "faces.db");
if (err != FSDKE_OK) {
    // Handle save error - log warning but continue cleanup
    printf("Warning: Failed to save tracker memory (error %d)\n", err);
}

// Step 2: Free all tracker handles
err = FSDK_FreeTracker(tracker);
if (err != FSDKE_OK) {
    printf("Warning: Failed to free tracker (error %d)\n", err);
}

// Step 3: Close all video cameras
err = FSDK_CloseVideoCamera(cameraHandle);
if (err != FSDKE_OK) {
    printf("Warning: Failed to close camera (error %d)\n", err);
}
```

<a id="cleanup-example-python"></a>
## Cleanup Example (Python)

```python
# Proper cleanup sequence in Python
try:
    # Save tracker memory
    tracker.SaveMemoryToFile("faces.db")
except Exception as e:
    print(f"Warning: Failed to save tracker memory: {e}")

try:
    # Free tracker
    FSDK.FreeTracker(tracker)
except Exception as e:
    print(f"Warning: Failed to free tracker: {e}")

try:
    # Close video camera
    FSDK.CloseVideoCamera(camera_handle)
except Exception as e:
    print(f"Warning: Failed to close camera: {e}")
```

<a id="best-practices"></a>
## Best Practices

- **Do not call SDK functions after FSDK_Finalize** — once finalized, calling any FaceSDK function results in undefined behavior. You must call [FSDK_Initialize](#fsdk_initialize-function) again before using the library.
- **Free images in loops** — if you process multiple images, free each `HImage` handle with [FSDK_FreeImage](#fsdk_freeimage-function) after processing to avoid accumulating memory. Do not wait until application exit.
- **Handle partial failures** — if one cleanup step fails, continue with the remaining steps. Log the error but do not skip subsequent cleanup calls.
- **Thread safety during cleanup** — ensure no other threads are calling FaceSDK functions when you begin the cleanup sequence. Wait for all processing threads to complete before starting cleanup.

<a id="configuration"></a>
# Configuration

<a id="fsdk_setparameter-function"></a>
## FSDK_SetParameter Function

Sets a parameter for FaceSDK. See the [FaceSDK Parameters](#facesdk-parameters) section for details.

Note that, to set Tracker parameters, the [FSDK_SetTrackerParameter](#fsdk_settrackerparameter-function) or [FSDK_SetTrackerMultipleParameters](#fsdk_settrackermultipleparameters-function) function should be used instead.

**C++ Syntax:**

```cpp
int FSDK_SetParameter(const char * ParameterName, const char * ParameterValue);
```

**Delphi Syntax:**

```delphi
function FSDK_SetParameter(ParameterName, ParameterValue: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetParameter(string ParameterName, string ParameterValue);
```

**Java and Android Syntax:**

```java
int FSDK.SetParameter(String ParameterName, String ParameterValue);
```

**Parameters:**

*ParameterName* - name of the parameter to be set.
*ParameterValue* - value of the parameter.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetParameter(param_name: str, param_value)
```

**Return Value:**

None

**Note:**

*param_value* can be one of the types: str, int, float or bool.

---

<a id="fsdk_setparameters-function"></a>
## FSDK_SetParameters Function

Sets multiple parameters for FaceSDK. The parameters and their values are specified in the following format:

```text
"Parameter1=Value1[;Parameter2=Value2[;...]]"
```

See the [FaceSDK Parameters](#facesdk-parameters) section for details.

**C++ Syntax:**

```cpp
int FSDK_SetParameters(const char * Parameters, int * ErrorPosition);
```

**Delphi Syntax:**

```delphi
function FSDK_SetParameters(Parameters: PAnsiChar; ErrorPosition: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetParameters(string Parameters, ref int ErrorPosition);
```

**Java and Android Syntax:**

```java
int FSDK.SetParameters(String Parameters, IntByReference ErrorPosition);
```

**Parameters:**

*Parameters* - string containing the parameters and the corresponding values to be set.
*ErrorPosition* - pointer to the integer variable that will receive the position of the character that caused the syntax error in the string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_SYNTAX_ERROR and sets the value of the ErrorPosition variable in case of syntax error.

**Example:**

```cpp
int err = 0;
FSDK_SetParameters("FaceDetectionModel=thermal.bin; TrimOutOfScreenFaces=false; TrimFacesWithUncertainFacialFeatures=false", &err);
```

**Python Syntax:**

```python
def FSDK.SetParameters(values='', **kwargs)
```

*values* - string containing the parameters and the corresponding values to be set separated by semicolon.
*kwargs* - keyword arguments as parameters with their values.

**Return Value:**

None

**Exceptions:**

FSDK.SyntaxError or FSDK.InvalidArgument if parameter(s) cannot be set.

**Examples:**

```python
FSDK_SetParameters("FaceDetectionModel=thermal.bin;TrimOutOfScreenFaces=false;TrimFacesWithUncertainFacialFeatures=false")

FSDK_SetParameters(FaceDetectionModel = "thermal.bin", TrimOutOfScreenFaces = False, TrimFacesWithUncertainFacialFeatures = False)
```

---

<a id="facesdk-parameters"></a>
## FaceSDK Parameters

FaceSDK allows for setting a number of parameters with the [FSDK_SetParameter](#fsdk_setparameter-function) or [FSDK_SetParameters](#fsdk_setparameters-function) function.

<a id="face-detection-parameters"></a>
### Face Detection Parameters

Note that the Tracker API does not use the face detection parameters set with [FSDK_SetParameter](#fsdk_setparameter-function) or [FSDK_SetParameters](#fsdk_setparameters-function). Instead, you should use [FSDK_SetTrackerParameter](#fsdk_settrackerparameter-function) or [FSDK_SetTrackerMultipleParameters](#fsdk_settrackermultipleparameters-function).

Also note that additional face detection parameters can be set by calling the [FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function) and [FSDK_SetFaceDetectionThreshold](#fsdk_setfacedetectionthreshold-function) functions.

| Parameter | Description |
|-----------|-------------|
| **FaceDetectionModel** | A path to the face detection model file to load. You can use it to load thermal face detection model (see the Thermal sample application). The value "default" can be passed to switch back to the default visual face detection model. |
| **TrimOutOfScreenFaces** | Determines whether faces that go beyond the edges of the image should be excluded from face detection. The default value is True (such faces aren't detected). Use True when you extract face templates from the detected faces and match them. Setting the value to False allows you to detect faces in a larger number of cases, but such faces may yield higher false acceptance rates when matching faces. |
| **TrimFacesWithUncertainFacialFeatures** | Determines whether faces with uncertain facial features should not be detected. The default value is True (faces with uncertain facial features aren't detected). Should be set to False for a thermal face detection model. Use True when you extract face templates from the detected faces and match them. Setting the value to False allows you to detect faces in a larger number of cases, but such faces may yield higher false acceptance rates when matching faces. |

<a id="working-with-images"></a>
# Working With Images

Images are represented as the HImage data type.

**C++ Declaration:**

```cpp
typedef int HImage;
```

**C# Declaration:**

```csharp
int Image
```

**Delphi Declaration:**

```pascal
HImage = integer;
PHImage = ^HImage;
```

**Java and Android Declaration:**

```java
class HImage {
    protected int himage;
};
```

**Python Declaration:**

```python
class Image(ctypes.Structure);
```

FaceSDK provides a number of functions to load images to the internal representation from files, buffers or HBITMAP handles and to save images from the internal representation to files, buffers and HBITMAP handles. Each FSDK_LoadImageFromXXXX function creates a new HImage handle, which can be deleted using the [FSDK_FreeImage](#fsdk_freeimage-function) function.

Note that when you perform multiple stages of recognition on large images (for example, when you first detect a face, and then create its template using FSDK_GetFaceTemplateInRegion), consider first resizing the image to a smaller size to speed up operations. Note that you must resize the image to dimensions no smaller than the InternalResizeWidth parameter of the FSDK_SetFaceDetectionParameters function if you perform face detection, in order to keep the same accuracy of face detection.

<a id="fsdk_createemptyimage-function"></a>
## FSDK_CreateEmptyImage Function

Creates a handle of an empty image. You don't need to call this function before calling FSDK_LoadImageFromXXXX since these functions already create the HImage handle. Should be called before using the [FSDK_CopyImage](#fsdk_copyimage-function), [FSDK_ResizeImage](#fsdk_resizeimage-function), [FSDK_RotateImage](#fsdk_rotateimage-function), [FSDK_RotateImageCenter](#fsdk_rotateimagecenter-function), [FSDK_RotateImage90](#fsdk_rotateimage90-function), [FSDK_MirrorImage](#fsdk_mirrorimage-function), [FSDK_CopyRect](#fsdk_copyrect-function), [FSDK_CopyRectReplicateBorder](#fsdk_copyrectreplicateborder-function) functions to create the handle of the destination image.

**C++ Syntax:**

```cpp
int FSDK_CreateEmptyImage(HImage* Image);
```

**Delphi Syntax:**

```pascal
function FSDK_CreateEmptyImage (Image: PHImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.CreateEmptyImage(ref int Image);
```

**Java and Android Syntax:**

```java
int FSDK.CreateEmptyImage(HImage Image);
```

**Parameters:**

*Image* - pointer to HImage for creating the image handle.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CreateEmptyImage() -> Image;
```

**Return Value:**

An empty image.

<a id="fsdk_loadimagefromfile-function"></a>
## FSDK_LoadImageFromFile Function

Loads the image from a file and provides the internal handle of this image.

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromFile(HImage* Image, char* FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromFile(Image: PHImage; FileName: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadImageFromFile(ref int Image, string FileName)
```

**Java and Android Syntax:**

```java
int FSDK.LoadImageFromFile(HImage Image, String FileName);
```

**CImage Syntax:**

```csharp
int Luxand.CImage(String FileName);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*FileName* - filename of the image to be loaded. FaceSDK supports the JPG, PNG and BMP file formats.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.LoadImageFromFile(fileName: str) -> Image;

// constructor
Image(fileName: str) -> Image;

@staticmethod
def Image.FromFile(fileName: str) -> Image;
```

**Return Value:**

An image loaded from file.

**Exceptions:**

- FSDK.FileNotFound
- FSDK.BadFileFormat
- FSDK.UnsupportedImageExtension
- FSDK.IOError

<a id="fsdk_loadimagefromfilew-function"></a>
## FSDK_LoadImageFromFileW Function

Loads the image from a file path in the Unicode character set and provides the internal handle of this image. The function is available only on Windows platforms.

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromFileW(HImage* Image, wchar_t* FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromFileW(Image: PHImage; FileName: PWideChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadImageFromFileW(ref int Image, string FileName)
```

**Java Syntax:**

```java
int FSDK.LoadImageFromFileW(HImage Image, String FileName);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*FileName* - filename of the image to be loaded. FaceSDK supports the JPG, PNG and BMP file formats.

**Return Value:**

Returns FSDKE_OK if successful.

This function is not available in Visual Basic 6.0.

<a id="fsdk_saveimagetofile-function"></a>
## FSDK_SaveImageToFile Function

Saves an image to a file. When saving to .jpg files, you can set the quality of JPEG compression using the [FSDK_SetJpegCompressionQuality](#fsdk_setjpegcompressionquality-function) function.

**C++ Syntax:**

```cpp
int FSDK_SaveImageToFile(HImage Image, char* FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveImageToFile(Image: HImage; FileName: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveImageToFile(int Image, string FileName);
```

**Java and Android Syntax:**

```java
int FSDK.SaveImageToFile(HImage Image, String FileName);
```

**CImage Syntax:**

```csharp
void Luxand.CImage.Save(string FileName);
```

**Parameters:**

*Image* - internal handle of an image to be saved.

*FileName* - name of file the image will be saved to. FaceSDK saves images in the BMP, PNG or JPG file format. The format to use is recognized by the extension specified in the FileName parameter.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
int img1;

FSDK_Initialize("");
FSDK_LoadImageFromFile(&img1, "test.bmp"); // load .bmp file
FSDK_SaveImageToFile(img1, "test.jpg"); // save as .jpg
```

**Python Syntax:**

```python
def FSDK.SaveImageToFile(image: Image, fileName: str, quality: int = None);

def Image.SaveToFile(fileName: str, quality: int = None);
```

**Return Value:**

None

**Exceptions:**

- FSDK.CannotCreateFile
- FSDK.IOError

**Example:**

```python
from fsdk import FSDK

FSDK.Initialize()
img = FSDK.Image("test.bmp") # load .bmp file
# if 'quality' is not defined the default or previously set value is used
img.SaveToFile("test.jpg", quality = 50) # save as .jpg
```

<a id="fsdk_saveimagetofilew-function"></a>
## FSDK_SaveImageToFileW Function

Saves an image to a file path in the Unicode character set. The function is available only on Windows platforms. When saving to .jpg files, you can set the quality of JPEG compression using the [FSDK_SetJpegCompressionQuality](#fsdk_setjpegcompressionquality-function) function.

**C++ Syntax:**

```cpp
int FSDK_SaveImageToFileW(HImage Image, wchar_t* FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveImageToFileW(Image: HImage; FileName: PWideChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveImageToFileW(int Image, string FileName);
```

**Java Syntax:**

```java
int FSDK.SaveImageToFileW(HImage Image, String FileName);
```

**Parameters:**

*Image* - internal handle of an image to be saved.

*FileName* - name of file the image will be saved to. FaceSDK saves images in the BMP, PNG or JPG file format. The format to use is recognized by the extension specified in the FileName parameter.

**Return Value:**

Returns FSDKE_OK if successful.

The function is not available in Visual Basic 6.0

<a id="fsdk_loadimagefrombuffer-function"></a>
## FSDK_LoadImageFromBuffer Function

Loads an image from a buffer and provides the internal handle of this image. The function suggests that the image data is organized in a top-to-bottom order, and the distance between adjacent rows is ScanLine bytes (for example, in the 24-bit image, the ScanLine value might be 3*Width bytes if there is no spacing between adjacent rows). The following image modes are supported:

| Mode name | Meaning |
|-----------|---------|
| FSDK_IMAGE_GRAYSCALE_8BIT | 8-bit grayscale image |
| FSDK_IMAGE_COLOR_24BIT | 24-bit color image (R, G, B order) |
| FSDK_IMAGE_COLOR_32BIT | 32-bit color image with alpha channel (R, G, B, A order) |

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromBuffer(HImage* Image, unsigned char* Buffer, int Width, int Height, int ScanLine, FSDK_IMAGEMODE ImageMode);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromBuffer(Image: PHImage; var Buffer; Width, Height: integer; ScanLine: integer; ImageMode: FSDK_IMAGEMODE): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadImageFromBuffer(ref int Image, byte[] Buffer, int Width, int Height, int ScanLine, FSDK_IMAGEMODE ImageMode);
```

**Android Syntax:**

```java
int FSDK.LoadImageFromBuffer(HImage Image, byte Buffer[], int Width, int Height, int ScanLine, FSDK_IMAGEMODE ImageMode);
```

**Java Syntax:**

```java
int FSDK.LoadImageFromBuffer(HImage Image, byte Buffer[], int Width, int Height, int ScanLine, int ImageMode);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*Buffer* - pointer to buffer containing image data.

*Width* - width of an image in pixels.

*Height* - height of an image in pixels.

*ScanLine* - distance between adjacent rows in bytes.

*ImageMode* - mode of an image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.LoadImageFromBuffer(buffer: bytes, width: int, height: int, scanLine: int, imageMode: int) -> Image;

@staticmethod
def Image.FromBuffer(buffer: bytes, width: int, height: int, scanLine: int, colorMode: int) -> Image;
```

**Return Value:**

An image loaded from buffer.

**Note:**

The constants FSDK.IMAGE_GRAYSCALE_8BIT, FSDK.IMAGE_COLOR_24BIT or FSDK.IMAGE_COLOR_32BIT are used as *imageMode* argument.

<a id="fsdk_loadimagefromjpegbuffer-function"></a>
## FSDK_LoadImageFromJpegBuffer Function

Loads an image from a buffer containing JPEG data, and provides the handle of this image.

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromJpegBuffer(HImage* Image, unsigned char* Buffer, unsigned int BufferLength);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromJpegBuffer(Image: PHImage; var Buffer; BufferLength: integer): integer;
```

**Android Syntax:**

```java
int FSDK.LoadImageFromJpegBuffer(HImage Image, byte Buffer[], int BufferLength);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*Buffer* - pointer to the buffer containing the image data in JPEG format (usually loaded from a JPEG file).

*BufferLength* - size of buffer in bytes.

**Return Value:**

Returns FSDKE_OK if successful.

This function is not available in .NET and Java.

**Python Syntax:**

```python
def FSDK.LoadImageFromJpegBuffer(buffer: bytes, bufferLength: int = None) -> Image;
```

**Return Value:**

An image loaded from jpeg buffer.

**Exception:**

FSDK.IOError

**Note:**

If *bufferLength* is not defined, an entire *buffer* is used.

<a id="fsdk_loadimagefrompngbuffer-function"></a>
## FSDK_LoadImageFromPngBuffer Function

Loads an image from a buffer containing PNG data, and provides the handle of this image.

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromPngBuffer(HImage* Image, unsigned char* Buffer, unsigned int BufferLength);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromPngBuffer(Image: PHImage; var Buffer; BufferLength: integer): integer;
```

**Android Syntax:**

```java
int FSDK.LoadImageFromPngBuffer(HImage Image, byte Buffer[], int BufferLength);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*Buffer* - pointer to the buffer containing the image data in PNG format (usually loaded from a PNG file).

*BufferLength* - size of buffer in bytes.

**Return Value:**

Returns FSDKE_OK if successful.

This function is not available in .NET and Java.

**Python Syntax:**

```python
def FSDK.LoadImageFromPngBuffer(buffer: bytes, bufferLength: int = None) -> Image;
```

**Return Value:**

An image loaded from png buffer.

**Exception:**

FSDK.IOError

**Note:**

If *bufferLength* is not defined, an entire *buffer* is used.

<a id="fsdk_getimagebuffersize-function"></a>
## FSDK_GetImageBufferSize Function

Returns the size of the buffer required to store an image.

**C++ Syntax:**

```cpp
int FSDK_GetImageBufferSize(HImage Image, int * BufSize, FSDK_IMAGEMODE ImageMode);
```

**Delphi Syntax:**

```pascal
function FSDK_GetImageBufferSize(Image: HImage; BufSize: PInteger; ImageMode: FSDK_IMAGEMODE): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetImageBufferSize(int Image, ref int BufSize, FSDK_IMAGEMODE ImageMode);
```

**Android Syntax:**

```java
int FSDK.GetImageBufferSize(HImage Image, int BufSize[], FSDK_IMAGEMODE ImageMode);
```

**Java Syntax:**

```java
int FSDK.GetImageBufferSize(HImage Image, int BufSize[], int ImageMode);
```

**Parameters:**

*Image* - internal handle of an image.

*BufSize* - pointer to an integer variable to store the calculated buffer size.

*ImageMode* - desired image mode of a buffer.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetImageBufferSize(image: image, imageMode: int) -> int;
```

**Return Value:**

The size of the buffer required to store an image.

<a id="fsdk_saveimagetobuffer-function"></a>
## FSDK_SaveImageToBuffer Function

Saves an image to a buffer in the desired image mode. Refer to the [FSDK_LoadImageFromBuffer](#fsdk_loadimagefrombuffer-function) function description to read more about image modes.

**C++ Syntax:**

```cpp
int FSDK_SaveImageToBuffer(HImage Image, unsigned char* Buffer, FSDK_IMAGEMODE ImageMode);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveImageToBuffer(Image: HImage; var Buffer; ImageMode: FSDK_IMAGEMODE): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveImageToBuffer(int Image,out byte[] Buffer, FSDK_IMAGEMODE ImageMode);
```

**Android Syntax:**

```java
int FSDK.SaveImageToBuffer(HImage Image, byte Buffer[], FSDK_IMAGEMODE ImageMode);
```

**Java Syntax:**

```java
int FSDK.SaveImageToBuffer(HImage Image, byte Buffer[], int ImageMode);
```

**Parameters:**

*Image* - internal handle of an image to be saved.

*Buffer* - pointer to the buffer containing the image data.

*ImageMode* - desired mode an image will be saved in.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def Image.ToBuffer(colorMode: int) -> bytes;
```

**Return Value:**

A buffer containing raw image data.

<a id="fsdk_loadimagefromhbitmap-function"></a>
## FSDK_LoadImageFromHBitmap Function

Loads the image from an HBITMAP handle and provides the internal handle of this image.

**C++ Syntax:**

```cpp
int FSDK_LoadImageFromHBitmap(HImage* Image, HBITMAP* BitmapHandle);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadImageFromHBitmap(Image: PHImage; BitmapHandle: HBitmap): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadImageFromHBitmap(ref int Image, IntPtr BitmapHandle);
```

**CImage Syntax:**

```csharp
Luxand.CImage(IntPtr BitmapHandle);
```

**Parameters:**

*Image* - pointer to HImage for receiving the loaded image handle.

*BitmapHandle* - handle of the image to be loaded.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.LoadImageFromHBitmap(bitmapHandle: HBITMAP) -> Image;

// constructor
Image(bitmapHandle: HBITMAP) -> Image;
```

**Return Value:**

An image created from HBITMAP Windows handle.

<a id="fsdk_saveimagetohbitmap-function"></a>
## FSDK_SaveImageToHBitmap Function

Creates an HBITMAP handle containing the image.

**C++ Syntax:**

```cpp
int FSDK_SaveImageToHBitmap(HImage Image, HBITMAP* BitmapHandle);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveImageToHBitmap(Image: HImage; BitmapHandle: PHBitmap): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveImageToHBitmap(Int Image, ref IntPtr BitmapHandle);
```

**CImage Syntax:**

```csharp
IntPtr Luxand.CImage.GetHbitmap();
```

**Parameters:**

*Image* - internal handle of the image to be saved to HBITMAP.

*BitmapHandle* - pointer to HBITMAP the created HBITMAP handle will be saved to.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SaveImageToHBitmap(image: Image) -> HBITMAP;

def Image.GetHBitmap() -> HBITMAP;
```

**Return Value:**

An HBITMAP Windows handle containg the image.

<a id="fsdkloadimagefromclrimage-function"></a>
## FSDK.LoadImageFromCLRImage Function

Loads the image from the System.Drawing.Image object and provides the internal handle of this image.

**C# Syntax:**

```csharp
int FSDK.LoadImageFromCLRImage(ref int Image, System.Drawing.Image ImageObject);
```

**CImage Syntax:**

```csharp
Luxand.CImage(System.Drawing.Image ImageObject);
```

**Parameters:**

*Image* - reference to HImage for receiving the loaded image handle.

*ImageObject* - object of the image to be loaded.

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdksaveimagetoclrimage-function"></a>
## FSDK.SaveImageToCLRImage Function

Creates a System.Drawing.Image object containing the image.

**C# Syntax:**

```csharp
int FSDK.SaveImageToCLRImage(int Image, ref System.Drawing.Image ImageObject);
```

**CImage Syntax:**

```csharp
System.Drawing.Image Luxand.CImage.ToCLRImage();
```

**Parameters:**

*Image* - internal handle of the image to be saved to System.Drawing.Image.

*ImageObject* - reference to System.Drawing.Image object the image will be saved to.

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdkloadimagefromawtimage-function"></a>
## FSDK.LoadImageFromAWTImage Function

Loads the image from the java.awt.Image object and provides the internal handle of this image.

**Java Syntax:**

```java
int FSDK.LoadImageFromAWTImage(HImage Image, java.awt.Image SourceImage, int ImageMode);
```

**Parameters:**

*Image* - HImage for receiving the loaded image.

*SourceImage* - java.awt.Image object of the image to be loaded.

*ImageMode* - mode of an image. (See [FSDK_LoadImageFromBuffer](#fsdk_loadimagefrombuffer-function) for more information about image modes.)

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdksaveimagetoawtimage-function"></a>
## FSDK.SaveImageToAWTImage Function

Creates a java.awt.Image object containing the image.

**Java Syntax:**

```java
int FSDK.SaveImageToAWTImage(HImage Image, java.awt.Image DestImage[], int ImageMode);
```

**Parameters:**

*Image* - internal handle of the image to be saved to java.awt.Image.

*DestImage[]* - java.awt.Image object the image will be saved to.

*ImageMode* - desired mode an image will be saved in.

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdk_setjpegcompressionquality-function"></a>
## FSDK_SetJpegCompressionQuality Function

Sets the quality of the JPEG compression to use in the [FSDK_SaveImageToFile](#fsdk_saveimagetofile-function) function.

**C++ Syntax:**

```cpp
int FSDK_SetJpegCompressionQuality(int Quality);
```

**Delphi Syntax:**

```pascal
function FSDK_SetJpegCompressionQuality(Quality: integer): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetJpegCompressionQuality(int Quality);
```

**Java and Android Syntax:**

```java
int FSDK.SetJpegCompressionQuality(int Quality);
```

**Parameters:**

*Quality* - quality of JPEG compression. Varies from 0 to 100.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetJpegCompressionQuality(quality: int);
```

**Return Value:**

None.

<a id="fsdk_getimagewidth-function"></a>
## FSDK_GetImageWidth Function

Returns the width of an image.

**C++ Syntax:**

```cpp
int FSDK_GetImageWidth(HImage SourceImage, int* Width);
```

**Delphi Syntax:**

```pascal
function FSDK_GetImageWidth(SourceImage: HImage; Width: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetImageWidth(int SourceImage, ref int Width);
```

**Java and Android Syntax:**

```java
int FSDK.GetImageWidth(HImage SourceImage, int Width[]);
```

**CImage Syntax:**

```csharp
int Luxand.CImage.Width;
```

**Parameters:**

*SourceImage* - internal handle of an image.

*Width* - pointer to an integer variable to store the width of an image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetImageWidth() -> int;

Image.width # property
Image.size # property for tuple (Image.width, Image.height)
```

**Return Value:**

The width of an image.

<a id="fsdk_getimageheight-function"></a>
## FSDK_GetImageHeight Function

Returns the height of an image.

**C++ Syntax:**

```cpp
int FSDK_GetImageHeight(HImage SourceImage, int* Height);
```

**Delphi Syntax:**

```pascal
function FSDK_GetImageHeight(SourceImage: HImage; Height: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetImageHeight(int SourceImage, ref int Height);
```

**Java and Android Syntax:**

```java
int FSDK.GetImageHeight(HImage SourceImage, int Height[]);
```

**CImage Syntax:**

```csharp
int Luxand.CImage.Height;
```

**Parameters:**

*SourceImage* - internal handle of an image.

*Height* - pointer to an integer variable to store the height of an image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetImageHeight() -> int;

Image.height # property
Image.size # property for tuple (Image.width, Image.height)
```

**Return Value:**

The height of an image.

<a id="fsdk_copyimage-function"></a>
## FSDK_CopyImage Function

Creates a copy of an image. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function.

**C++ Syntax:**

```cpp
int FSDK_CopyImage(HImage SourceImage, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_CopyImage(SourceImage: HImage; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.CopyImage(int SourceImage, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.CopyImage(HImage SourceImage, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.Copy();
```

**Parameters:**

*SourceImage* - handle of an image to be copied.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CopyImage(sourceImage: Image, destImage: Image) -> Image;

def Image.Copy() -> Image;
```

**Return Value:**

The new copy of an image.

<a id="fsdk_resizeimage-function"></a>
## FSDK_ResizeImage Function

Changes the size of an image. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function.

**C++ Syntax:**

```cpp
int FSDK_ResizeImage(HImage SourceImage, double ratio, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_ResizeImage(SourceImage: HImage; ratio: double; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.ResizeImage(int SourceImage, double ratio, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.ResizeImage(HImage SourceImage, double ratio, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.Resize(double ratio);
```

**Parameters:**

*SourceImage* - handle of an image to be resized.

*ratio* - factor by which the x and y dimensions of the source image are changed. A factor value greater than 1 corresponds to increasing the image size.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.ResizeImage(sourceImage: Image, ratio: float, destImage: Image) -> Image;

def Image.Resize(ratio: float) -> Image;
```

**Return Value:**

The new resized image.

<a id="fsdk_rotateimage-function"></a>
## FSDK_RotateImage Function

Rotates an image around its center. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function.

**C++ Syntax:**

```cpp
int FSDK_RotateImage(HImage SourceImage, double angle, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_RotateImage(SourceImage: HImage; angle: double; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.RotateImage(int SourceImage, double angle, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.RotateImage(HImage SourceImage, double angle, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.Rotate(double angle);
```

**Parameters:**

*SourceImage* - handle of an image to be rotated.

*angle* - rotation angle in degrees.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.RotateImage(sourceImage: Image, angle: float, destImage: Image) -> Image;

def Image.Rotate(angle: float) -> Image;
```

**Return Value:**

The new rotated image.

<a id="fsdk_rotateimagecenter-function"></a>
## FSDK_RotateImageCenter Function

Rotates an image around an arbitrary center. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function.

**C++ Syntax:**

```cpp
int FSDK_RotateImageCenter(HImage SourceImage, double angle, double xCenter, double yCenter, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_RotateImageCenter(SourceImage: HImage; angle: double; xCenter: double; yCenter: double; DestImage: HImage;): integer;
```

**C# Syntax:**

```csharp
int FSDK.RotateImageCenter(int SourceImage, double angle, double xCenter, double yCenter, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.RotateImageCenter(HImage SourceImage, double angle, double xCenter, double yCenter, HImage DestImage);
```

**Parameters:**

*SourceImage* - handle of an image to be rotated.

*angle* - rotation angle in degrees.

*xCenter* - the X coordinate of the rotation center.

*yCenter* - the Y coordinate of the rotation center.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.RotateImageCenter(sourceImage: Image, angle: float, xCenter: float, yCenter: float, destImage: Image) -> Image;

def Image.RotateCenter(angle: float, xc: float, yc: float) -> Image;
```

**Return Value:**

The new rotated image.

<a id="fsdk_rotateimage90-function"></a>
## FSDK_RotateImage90 Function

Rotates the image by 90 or 180 degrees clockwise or counter-clockwise. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function.

**C++ Syntax:**

```cpp
int FSDK_RotateImage90(HImage SourceImage, int Multiplier, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_RotateImage90(SourceImage: HImage; Multiplier: integer; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.RotateImage90(int SourceImage, int Multiplier, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.RotateImage90(HImage SourceImage, int Multiplier, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.Rotate90(int Multiplier);
```

**Parameters:**

*SourceImage* - handle of an image to be rotated.

*Multiplier* - an integer multiplier of 90 degrees defining the rotation angle. Specify 1 for 90 degrees clockwise, 2 for 180 degrees clockwise; specify -1 for 90 degrees counter-clockwise.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.RotateImage90(sourceImage: Image, multiplier: int, destImage: Image) -> Image;

def Image.Rotate90(multiplier: int = 1) -> Image;
```

**Return Value:**

The new rotated image.

<a id="fsdk_copyrect-function"></a>
## FSDK_CopyRect Function

Creates a copy of a rectangular area of an image. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function. If some apex of a rectangle is located outside the source image, rectangular areas that do not contain the source image will be black.

**C++ Syntax:**

```cpp
int FSDK_CopyRect(HImage SourceImage, int x1, int y1, int x2, int y2, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_CopyRect(SourceImage: HImage; x1, y1, x2, y2: integer; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.CopyRect(int SourceImage, int x1, int y1, int x2, int y2, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.CopyRect(HImage SourceImage, int x1, int y1, int x2, int y2, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.CopyRect(int x1, int y1, int x2, int y2);
```

**Parameters:**

*SourceImage* - handle of an image to be rotated.

*x1* - the X coordinate of the bottom left corner of the copied rectangle.

*y1* - the Y coordinate of the bottom left corner of the copied rectangle.

*x2* - the X coordinate of the top right corner of the copied rectangle.

*y2* - the Y coordinate of the top right corner of the copied rectangle.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CopyRect(sourceImage: Image, x1: int, y1: int, x2: int, y2: int, destImage: Image) -> Image;

def Image.CopyRect(x1: int, y1: int, x2: int, y2: int) -> Image;
```

**Return Value:**

The new cropped image.

<a id="fsdk_copyrectreplicateborder-function"></a>
## FSDK_CopyRectReplicateBorder Function

Creates a copy of a rectangular area of an image and adds replicated border pixels. The handle of the destination image should be created with the [FSDK_CreateEmptyImage](#fsdk_createemptyimage-function) function. This function copies the source image to the destination image and fills pixels ("border") outside the copied area in the destination image with the values of the nearest source image pixels.

**C++ Syntax:**

```cpp
int FSDK_CopyRectReplicateBorder(HImage SourceImage, int x1, int y1, int x2, int y2, HImage DestImage);
```

**Delphi Syntax:**

```pascal
function FSDK_CopyRectReplicateBorder(SourceImage: HImage; x1, y1, x2, y2: integer; DestImage: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.CopyRectReplicateBorder(int SourceImage, int x1, int y1, int x2, int y2, int DestImage);
```

**Java and Android Syntax:**

```java
int FSDK.CopyRectReplicateBorder(HImage SourceImage, int x1, int y1, int x2, int y2, HImage DestImage);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.CopyRectReplicateBorder(int x1, int y1, int x2, int y2);
```

**Parameters:**

*SourceImage* - handle of an image to be rotated.

*x1* - the X coordinate of the bottom left corner of the copied rectangle.

*y1* - the Y coordinate of the bottom left corner of the copied rectangle.

*x2* - the X coordinate of the top right corner of the copied rectangle.

*y2* - the Y coordinate of the top right corner of the copied rectangle.

*DestImage* - handle of the destination image.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CopyRectReplicateBorder(sourceImage: Image, x1: int, y1: int, x2: int, y2: int, destImage: Image) -> Image;

def Image.CopyRectReplicateBorder(x1: int, y1: int, x2: int, y2: int) -> Image;
```

**Return Value:**

The new cropped image.

<a id="fsdk_mirrorimage-function"></a>
## FSDK_MirrorImage Function

Mirrors an image. The function can mirror horizontally and vertically.

**C++ Syntax:**

```cpp
int FSDK_MirrorImage(HImage Image, bool UseVerticalMirroringInsteadOfHorizontal);
```

**Delphi Syntax:**

```pascal
function FSDK_MirrorImage(Image: HImage; UseVerticalMirroringInsteadOfHorizontal: boolean): integer;
```

**C# Syntax:**

```csharp
int FSDK.MirrorImage(int Image, bool UseVerticalMirroringInsteadOfHorizontal);
```

**Java and Android Syntax:**

```java
int FSDK.MirrorImage(HImage Image, boolean UseVerticalMirroringInsteadOfHorizontal);
```

**CImage Syntax:**

```csharp
Luxand.CImage Luxand.CImage.MirrorVertical();
Luxand.CImage Luxand.CImage.MirrorHorizontal();
```

**Parameters:**

*Image* - handle of the image to be mirrored.

*UseVerticalMirroringInsteadOfHorizontal* - sets the mirror direction.

**TRUE:** left-to-right swap;

**FALSE:** top-to-bottom swap;

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.MirrorImage(image: Image, useVerticalMirroringInsteadOfHorizontal: bool = False) -> Image;

def Image.Mirror(useVerticalMirroringInsteadOfHorizontal: bool = False) -> Image;
```

**Return Value:**

Mirrored image.

<a id="fsdk_freeimage-function"></a>
## FSDK_FreeImage Function

Frees the internal representation of an image.

**C++ Syntax:**

```cpp
int FSDK_FreeImage(HImage Image);
```

**Delphi Syntax:**

```pascal
function FSDK_FreeImage(Image: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.FreeImage(int Image);
```

**Java and Android Syntax:**

```java
int FSDK.FreeImage(HImage Image);
```

**Parameters:**

*Image* - handle of the image to be freed.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.FreeImage(image: Image):

def Image.Free();
```

**Return Value:**

None.

**Note:**

The image will be freed automatically if it is not freed by hand.

<a id="face-detection"></a>
# Face Detection

You can use the [FSDK_DetectFace](#fsdk_detectface-function) function to detect a frontal face in an image. The function returns the position of the face in the image. The performance and reliability of face detection is controlled by the [FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function) and [FSDK_SetFaceDetectionThreshold](#fsdk_setfacedetectionthreshold-function) functions.

Typical parameters for face detection are:

- To detect faces from a webcam in real time, call:
  ```
  FSDK_SetFaceDetectionParameters(false, false, 100);
  ```

- To reliably detect faces in digital camera photos, call:
  ```
  FSDK_SetFaceDetectionParameters(true, false, 500);
  ```

<a id="face-detection-models"></a>
## Face Detection Models

Luxand FaceSDK allows you to switch the internal models used for face detection. You may use the switching to load improved face detection models when made available by Luxand or to switch to a thermal face detection model.

Use the FSDK_SetParameter or FSDK_SetParameters function to load a face detection model from a file. When using Tracker API, use the FSDK_SetTrackerParameter or FSDK_SetTrackerMultipleParameters function instead. Set the FaceDetectionModel parameter to specify the file to load a model from. Be sure to check the return value of FSDK_SetParameter or FSDK_SetParameters to confirm the file loaded correctly.

To load a thermal face detection model, set FaceDetectionModel to `thermal.bin`. Confirm this file is available in the current directory and, if not, specify the full path to the file.

To switch back to the default model (i.e., the model for visual face detection), set FaceDetectionModel to `default`. See the FaceSDK Parameters section for more information.

<a id="face-detection-on-thermal-images"></a>
## Face Detection on Thermal Images

Luxand FaceSDK allows for the detection of faces on 8-bit grayscale thermal images. You typically receive such images from a thermal camera, with each pixel representing temperature.

To pass the thermal image to FaceSDK, you may need to convert the temperature values of the image (which may be float or 14-bit values, for example) into 8-bit values (from 0 to 255). The absolute temperature itself is not taken into account by FaceSDK when detecting faces, only the relative difference in temperature between facial features and the background.

Typically, you may normalize an image so that coldest pixel is represented by 0 and the hottest by 255. However, if you have very hot or very cold images in the background, this may lead to faces having a low contrast. Therefore, it is recommended to normalize the image so that 0 would represent the temperature of about 20 degrees Celsius and 255 the temperature of about 40 degrees Celsius (the usual range of temperatures for human faces). After this normalization, any pixels colder than 20 degrees Celsius will have the value 0, and any pixels hotter than 40 degrees Celsius will have the value of 255.

If your thermal camera returns a noisy picture, you may get lower detection rates. In such cases, it is recommended to de-noise the image with a median or a Gaussian filter before passing it to FaceSDK. More information can be found on the links below:
- [https://en.wikipedia.org/wiki/Median_filter](https://en.wikipedia.org/wiki/Median_filter)
- [https://en.wikipedia.org/wiki/Gaussian_blur](https://en.wikipedia.org/wiki/Gaussian_blur)

Try varying the face detection threshold if you get a high number of false positives or low detection rates on your camera.

FaceSDK itself does not communicate with thermal cameras except when the camera is available as a standard Windows web camera. When working with a thermal camera, you need to use the camera manufacturer's API to receive images. To pass thermal images to FaceSDK, you may use the FSDK_LoadImageFromBuffer function after converting the images to an 8-bit format (and possibly normalizing the pixel values, as described above).

To detect faces on thermal images, follow these steps:

1. Load a face detection model by setting the FaceDetectionModel with the FSDK_SetParameter or FSDK_SetParameters function. If using Tracker API, use the FSDK_SetTrackerParameter or FSDK_SetTrackerMultipleParameters function instead.
2. Check the return value of the above functions for error to be sure the thermal model was loaded.
3. Set the `TrimOutOfScreenFaces` and `TrimFacesWithUncertainFacialFeatures` parameters to False using the same functions.
4. Pass thermal images to FSDK_DetectFaces, FSDK_DetectMultipleFaces or FSDK_FeedFrame (when using Tracker API).

**Example:**

```cpp
FSDK_SetParameters("FaceDetectionModel=thermal.bin; TrimOutOfScreenFaces=false; TrimFacesWithUncertainFacialFeatures=false", &err);
```

Refer to the Thermal sample application to see how faces on thermal images can be detected.

<a id="data-types"></a>
## Data types

Luxand FaceSDK introduces the TFacePosition data type that stores the information about the position of the face. The `xc` and `yc` fields specifies the X and Y coordinates of the center of the face, `w` specifies the width of the face, and `angle` specifies the in-plane rotation angle of the face in degrees.

**C++ Declaration:**

```cpp
typedef struct {
    int xc, yc, w;
    int padding;
    double angle;
} TFacePosition;
```

**C# Declaration:**

```csharp
public struct TFacePosition {
    public int xc, yc, w;
    public double angle;
}
```

**Delphi Declaration:**

```pascal
TFacePosition = record
   xc, yc, w: integer;
   padding: integer;
   angle: double;
end;
PFacePosition = ^TFacePosition;
```

**Java Declaration:**

The class TFacePosition contains the following fields:

```java
   public int xc, yc, w;
   public double angle;
```

The class TFaces encapsulates an array of TFacePosition classses. It has the following properties:

```java
   public TFacePosition faces[];
   int maxFaces;
```

**Python Declaration:**

```python
class FSDK.FacePosition(ctypes.Structure):
    _fields_ = ("xc", c_int), ("yc", c_int), ("w", c_int), ("_padding", c_int), ("angle", c_double)
    @property
    def rect(self):
        """ the rect of face as tuple (x1, y1, x2, y2)"""
        x, y, w = self.xc, self.yc, self.w//2
        return x-w, y-w, x+w, y+w
```

<a id="fsdk_detectface-function"></a>
## FSDK_DetectFace Function

Detects a frontal face in an image and stores information about the face position into the TFacePosition structure.

**C++ Syntax:**

```cpp
int FSDK_DetectFace(HImage Image, TFacePosition* FacePosition);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectFace(Image: HImage; FacePosition: PFacePosition): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectFace(int Image, ref FSDK.TFacePosition FacePosition);
```

**Java Syntax:**

```java
int FSDK.DetectFace(HImage Image, TFacePosition.ByReference FacePosition);
```

**Android Syntax:**

```java
int FSDK.DetectFace(HImage Image, TFacePosition FacePosition);
```

**CImage Syntax:**

```csharp
Luxand.TFacePosition Luxand.CImage.DetectFace();
```

**Parameters:**

- **Image** - handle of the image to detect the face in.
- **FacePosition** - pointer to the TFacePosition structure to store information about the face position.

**Return Value:**

Returns FSDKE_OK if successful. If a face is not found, the function returns the FSDKE_FACE_NOT_FOUND code. If the input image is too small (less than 20x20 pixels), the functions returns FSDKE_IMAGE_TOO_SMALL.

**Example:**

```cpp
HImage img1;
TFacePosition FacePosition;

FSDK_Initialize("");
FSDK_ActivateLibrary("your-license-key-here");
FSDK_LoadImageFromFile(&img1, "test.jpg");

int err = FSDK_DetectFace(img1, &FacePosition);
if (err == FSDKE_OK) {
    printf("face position: %d %d %.1f\n", FacePosition.xc, FacePosition.yc, FacePosition.angle);
} else if (err == FSDKE_FACE_NOT_FOUND) {
    printf("No face found in the image\n");
}

FSDK_FreeImage(img1);
```

**Python Syntax:**

```python
def FSDK.DetectFace(image: Image) -> FacePosition;

def Image.DetectFace() -> FacePosition;
```

Both forms are equivalent — `Image.DetectFace()` is a convenience method that calls `FSDK.DetectFace(image)` internally.

**Return Value:**

FacePosition object.

**Exception:**

- FSDK.FaceNotFound — raised when no face is detected in the image
- FSDK.ImageTooSmall — raised when the image is smaller than 20x20 pixels

**Example:**

```python
from fsdk import FSDK

image = FSDK.Image("test.jpg")

try:
    face = image.DetectFace()
    print(f"face position: {face.xc} {face.yc} {face.angle:.1f}")
except FSDK.FaceNotFound:
    print("No face found in the image")

FSDK.FreeImage(image)
```

<a id="fsdk_detectmultiplefaces-function"></a>
## FSDK_DetectMultipleFaces Function

Detects multiple faces in an image.

**C++ Syntax:**

```cpp
int FSDK_DetectMultipleFaces(HImage Image, int* DetectedCount, TFacePosition* FaceArray, int MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectMultipleFaces(Image: HImage; DetectedCount: PInteger; FaceArray: PFacePositionArray; MaxSizeInBytes: integer): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectMultipleFaces(int Image, ref int DetectedCount, out FSDK.TFacePosition[] FaceArray, int MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.DetectMultipleFaces(HImage Image, TFaces FaceArray);
```

**CImage Syntax:**

```csharp
Luxand.TFacePosition[] Luxand.CImage.DetectMultipleFaces();
```

**Parameters:**

- **Image** - handle of the image to detect faces in.
- **DetectedCount** - count of the faces found in the image.
- **FaceArray** - pointer to the array of TFacePosition structure to store the information about the detected faces.
- **MaxSizeInBytes** - size of the FaceArray buffer in bytes. The function will not store more than MaxSize bytes in the buffer.

**Return Value:**

Returns FSDKE_OK if successful. If no faces are found, the function returns the FSDKE_FACE_NOT_FOUND code. If the input image is too small (less than 20x20 pixels), the functions returns FSDKE_IMAGE_TOO_SMALL.

**Example:**

```cpp
HImage img1;
int DetectedCount;
TFacePosition FaceArray[50];

FSDK_Initialize("");
FSDK_ActivateLibrary("your-license-key-here");
FSDK_LoadImageFromFile(&img1, "test.jpg");

int err = FSDK_DetectMultipleFaces(img1, &DetectedCount, FaceArray, sizeof(FaceArray));
if (err == FSDKE_OK) {
    for (int i = 0; i < DetectedCount; i++) {
        printf("face position: %d %d %.1f\n", FaceArray[i].xc, FaceArray[i].yc, FaceArray[i].angle);
    }
} else if (err == FSDKE_FACE_NOT_FOUND) {
    printf("No faces found in the image\n");
}

FSDK_FreeImage(img1);
```

**Python Syntax:**

```python
def FSDK.DetectMultipleFaces(image: Image) -> List[FacePosition];

def Image.DetectMultipleFaces() -> List[FacePosition];
```

**Return Value:**

A list of FacePosition objects. Returns an empty list if no faces are found (no exception is raised, unlike `DetectFace()`).

**Exception:**

- FSDK.ImageTooSmall — raised when the image is smaller than 20x20 pixels

**Example:**

```python
from fsdk import FSDK

image = FSDK.Image("test.jpg")
faces = image.DetectMultipleFaces()

if len(faces) > 0:
    for face in faces:
        print(f"face position: {face.xc} {face.yc} {face.angle:.1f}")
else:
    print("No faces found in the image")

FSDK.FreeImage(image)
```

<a id="fsdk_setfacedetectionparameters-function"></a>
## FSDK_SetFaceDetectionParameters Function

Allows setting a number of face detection parameters to control the performance and reliability of face detector.

The function allows configuring the following parameters: HandleArbitraryRotations, DetermineFaceRotationAngle and InternalResizeWidth.

HandleArbitraryRotations, DetermineFaceRotationAngle can be TRUE or FALSE, while InternalResizeWidth is an integer.

Other face detection parameters that can also be set using the FSDK_SetParameter or FSDK_SetParameters function.

**C++ Syntax:**

```cpp
int FSDK_SetFaceDetectionParameters(bool HandleArbitraryRotations, bool DetermineFaceRotationAngle, int InternalResizeWidth);
```

**Delphi Syntax:**

```pascal
function FSDK_SetFaceDetectionParameters(HandleArbitraryRotations: boolean; DetermineFaceRotationAngle: boolean; InternalResizeWidth: integer): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetFaceDetectionParameters(bool HandleArbitraryRotations, bool DetermineFaceRotationAngle, int InternalResizeWidth);
```

**Java and Android Syntax:**

```java
int FSDK.SetFaceDetectionParameters(boolean HandleArbitraryRotations, boolean DetermineFaceRotationAngle, int InternalResizeWidth);
```

**Parameters:**

**HandleArbitraryRotations** - extends default in-plane face rotation angle from -15..15 degrees to -30..30 degrees.

**TRUE**: extended in-plane rotation support is enabled at the cost of detection speed (3 times performance hit).

**FALSE**: default fast detection -15..15 degrees.

**DetermineFaceRotationAngle** - enables or disables the detection of in-plane face rotation angle.

**TRUE**: detects in-plane rotation angle when detecting faces. The angle is recorded into the Angle field of the TFacePosition structure (TFacePosition is a structure returned by [FSDK_DetectFace](#fsdk_detectface-function) and [FSDK_DetectMultipleFaces](#fsdk_detectmultiplefaces-function)).

**FALSE**: disables the detection of rotation angle.

*Note: Enabling face rotation angle detection slows down the detection process slightly. Set this parameter to TRUE if you are planning to call FSDK_DetectFacialFeatures or FSDK_DetectFacialFeaturesInRegion.*

**InternalResizeWidth** - controls the detection speed by setting the size of the image the detection functions will work with. Choose higher value to increase detection quality, or lower value to improve the performance.

*Note: By default, all images are internally resized to the width of 384 pixels. 384 pixels are a reasonable compromise between performance and detection quality. While large images are down-sized, the smaller ones are up-sized to the specified Resize Width in order to maintain constant detection speed.*

<a id="choosing-the-right-value-for-internalresizewidth"></a>
### Choosing the right value for InternalResizeWidth

Choosing the correct value for the InternalResizeWidth parameter is essential for the correct operation of face detection functions of the SDK. The face detection functions can only detect faces as small as 20x20 pixels. Even if the source image is a large 1000x1000 dots one, the face on that image can be as small as 100x100 pixels. If you set InternalResizeWidth to 200, then the source image will be resized to 200x200 pixels, thus the face will only occupy 20x20 pixels. This is still enough for the SDK functions to work. If, however, you set InternalResizeWidth to 100, then the original image will become 100x100 pixels, and the face on it will only occupy 10x10 dots, which is NOT enough for the SDK functions to work with.

Be extra careful when changing the default value of InternalResizeWidth. For example, webcam images can be usually detected with InternalResizeWidth set to 100, while images from multi-megapixel digital cameras require values of at least 384 or 512 pixels to work with.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetFaceDetectionParameters(handleArbitraryRotations: bool, determineFaceRotationAngle: bool, internalResizeWidth: int);
```

**Return Value:**

None.

---

<a id="complete-face-detection-workflow"></a>
## Complete Face Detection Workflow

This section demonstrates the full workflow for loading an image and detecting all faces.

<a id="complete-example-c"></a>
### Complete Example (C++)

```cpp
// Initialize and activate the SDK
FSDK_Initialize("");
FSDK_ActivateLibrary("your-license-key-here");

// Configure face detection parameters
// Enable rotation handling, resize width 384
FSDK_SetFaceDetectionParameters(true, true, 384);

// Load the image
HImage imageHandle;
int err = FSDK_LoadImageFromFile(&imageHandle, "photo.jpg");
if (err != FSDKE_OK) {
    printf("Error loading image: %d\n", err);
    return;
}

// Detect all faces in the image
int detectedCount;
TFacePosition faceArray[100];
err = FSDK_DetectMultipleFaces(imageHandle, &detectedCount, faceArray, sizeof(faceArray));

if (err == FSDKE_OK) {
    printf("Detected %d face(s)\n", detectedCount);
    for (int i = 0; i < detectedCount; i++) {
        printf("  Face %d: center=(%d, %d), width=%d, angle=%.1f\n",
            i + 1, faceArray[i].xc, faceArray[i].yc,
            faceArray[i].w, faceArray[i].angle);
    }
} else if (err == FSDKE_FACE_NOT_FOUND) {
    printf("No faces detected in the image\n");
} else if (err == FSDKE_IMAGE_TOO_SMALL) {
    printf("Error: image is too small (minimum 20x20 pixels)\n");
}

// Clean up
FSDK_FreeImage(imageHandle);
```

<a id="complete-example-python"></a>
### Complete Example (Python)

```python
from fsdk import FSDK

# Initialize and activate the SDK
FSDK.Initialize()
FSDK.ActivateLibrary("your-license-key-here")

# Configure face detection parameters
# Enable rotation handling, resize width 384
FSDK.SetFaceDetectionParameters(True, True, 384)

# Load the image
image = FSDK.Image("photo.jpg")

# Detect all faces in the image
faces = image.DetectMultipleFaces()

if len(faces) > 0:
    print(f"Detected {len(faces)} face(s)")
    for i, face in enumerate(faces):
        print(f"  Face {i+1}: center=({face.xc}, {face.yc}), width={face.w}, angle={face.angle:.1f}")
else:
    print("No faces detected in the image")

# Clean up
FSDK.FreeImage(image)
```

<a id="error-handling-notes"></a>
### Error Handling Notes

- **FSDKE_OK** — faces detected successfully
- **FSDKE_FACE_NOT_FOUND** — no faces found in the image (not an error; the image simply contains no detectable faces)
- **FSDKE_IMAGE_TOO_SMALL** — the image dimensions are below the minimum of 20x20 pixels
- Always call `FSDK_FreeImage` for every loaded image to avoid memory leaks, even if detection fails
- In Python, `DetectMultipleFaces()` returns an empty list when no faces are found (no exception is raised), while `DetectFace()` raises `FSDK.FaceNotFound`

<a id="fsdk_setfacedetectionthreshold-function"></a>
## FSDK_SetFaceDetectionThreshold Function

Sets a threshold value for face detection. The default value is 5. The lowest possible value is 1.

The function allows adjusting the sensitivity of the detection. If the threshold value is set to a higher value, the detector will only recognize faces with sharp, clearly defined details, thus reducing the number of false positive detections. Setting the threshold lower allows detecting more faces with less clearly defined features at the expense of increased number of false positives.

**C++ Syntax:**

```cpp
int FSDK_SetFaceDetectionThreshold(int Threshold);
```

**Delphi Syntax:**

```pascal
function FSDK_SetFaceDetectionThreshold(Threshold: integer): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetFaceDetectionThreshold(int Threshold);
```

**Java and Android Syntax:**

```java
int FSDK.SetFaceDetectionThreshold(int Threshold);
```

**Parameters:**

**Threshold** - Threshold value.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetFaceDetectionThreshold(threshold: int);
```

**Return Value:**

None.

<a id="facial-feature-detection"></a>
# Facial Feature Detection

FaceSDK provides the [FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function) function to detect facial features in an image and the [FSDK_DetectEyes](#fsdk_detecteyes-function) function to detect just eye centers in an image. First, these functions detect a frontal face in an image, and then detect its facial features or only eye centers. The [FSDK_DetectFacialFeaturesInRegion](#fsdk_detectfacialfeaturesinregion-function) and [FSDK_DetectEyesInRegion](#fsdk_detecteyesinregion-function) functions do not perform the face detection step and detect facial features or eye centers in a region returned by FSDK_DetectFace or FSDK_DetectMultipleFaces.

In the current version of Luxand FaceSDK the performance of [FSDK_DetectEyes](#fsdk_detecteyes-function) and [FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function) is the same, so there is no advantage in calling [FSDK_DetectEyes](#fsdk_detecteyes-function) instead of [FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function).

The facial features are stored in the FSDK_Features data structure. FSDK_Features is an array data type containing FSDK_FACIAL_FEATURE_COUNT points. The list of facial features recognized by FaceSDK is available in the Detected Facial Features chapter.

Eye centers are saved to FSDK_Features[0] and FSDK_Features[1]. The [FSDK_DetectEyes](#fsdk_detecteyes-function) and [FSDK_DetectEyesInRegion](#fsdk_detecteyesinregion-function) functions do not change other elements of the FSDK_Features array.

<a id="data-types"></a>
## Data Types

**C++ Declaration:**

```cpp
typedef struct { int x,y; } TPoint;
typedef TPoint FSDK_Features [FSDK_FACIAL_FEATURE_COUNT];
```

**C# Declaration:**

```csharp
public struct TPoint {
    public int x, y;
}
```

**Delphi Declaration:**

```pascal
TPoint = record
    x, y: integer;
end;
FSDK_Features = array[0..FSDK_FACIAL_FEATURE_COUNT - 1] of TPoint;
PFSDK_Features = ^FSDK_Features;
```

**Java and Android Declaration:**

The class TPoint has the following properties:

```java
public int x, y;
```

The class FSDK_Features has the following property:

```java
public TPoint features[];
```

**Python Declaration:**

```python
class Point(ctypes.Structure):
    fields_ = ("x", c_int), ("y", c_int)
Features = Point*FSDK.FSDK_FACIAL_FEATURE_COUNT
```

<a id="fsdk_detectfacialfeatures-function"></a>
## FSDK_DetectFacialFeatures Function

Detects a frontal face in an image and detects its facial features.

**C++ Syntax:**

```cpp
int FSDK_DetectFacialFeatures(HImage Image, FSDK_Features* FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectFacialFeatures(Image: HImage; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectFacialFeatures(int Image, out FSDK.TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.DetectFacialFeatures(HImage Image, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.DetectFacialFeatures(HImage Image, FSDK_Features FacialFeatures);
```

**CImage Syntax:**

```csharp
FSDK.TPoint[] Luxand.CImage.DetectFacialFeatures();
```

**Parameters:**

- **Image** - handle of the image facial features should be detected in.
- **FacialFeatures** - pointer to the FSDK_Features array for receiving the detected facial features.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
int img1;
FSDK_Features Features;

FSDK_Initialize("");
FSDK_LoadImageFromFile(&img1, "test.jpg");
FSDK_DetectFacialFeatures(img1, Features);

printf("Left eye location: (%d, %d)\n", Features[FSDKP_LEFT_EYE].x, Features[FSDKP_LEFT_EYE].y);
printf("Right eye location: (%d, %d)\n", Features[FSDKP_RIGHT_EYE].y, Features[FSDKP_RIGHT_EYE].y);
```

**Python Syntax:**

```python
def FSDK.DetectFacialFeatures(image: Image) -> Features;

def Image.DetectFacialFeatures(image: Image, facePosition: FacePosition = None, *, confidenceLevels = False) -> Features;
```

**Return Value:**

The Features object.

**Exception:**

FSDK.FaceNotFound

**Note:**

If *facePosition* is None the function detects a frontal face in an image and returns its facial features.

If *facePosition* is defined the function detects facial features of a specific face in a region returned by FSDK.DetectFace or FSDK.DetectMultipleFace.

If *confidenceLevel* is True the returned 'Features' objects contains the *confidenceLevel* attribute represented by an array of floats that holds confidence levels of each facial feature.

**Python Example:**

```python
from fsdk import FSDK

FSDK.Initialize()
features = FSDK.Image("test.jpg").DetectFacialFeatures()
print(f"Left eye location: {features[FSDK.FSDKP_LEFT_EYE]}")
print(f"Right eye location: {features[FSDK.FSDKP_RIGHT_EYE]}")
```

<a id="fsdk_detectfacialfeaturesinregion-function"></a>
## FSDK_DetectFacialFeaturesInRegion Function

Detects facial features in an image region returned by FSDK_DetectFace or FSDK_DetectMultipleFaces. This function can be useful if an approximate face size is known, or to detect facial features of a specific face returned by FSDK_DetectMultipleFaces.

**C++ Syntax:**

```cpp
int FSDK_DetectFacialFeaturesInRegion(HImage Image, TFacePosition* FacePosition, FSDK_Features* FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectFacialFeaturesInRegion(Image: HImage; FacePosition: PFacePosition; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectFacialFeaturesInRegion(int Image, ref FSDK.TFacePosition FacePosition, out FSDK.TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.DetectFacialFeaturesInRegion(HImage Image, TFacePosition FacePosition, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.DetectFacialFeaturesInRegion(HImage Image, TFacePosition FacePosition, FSDK_Features FacialFeatures);
```

**C# Syntax:**

```csharp
FSDK.TPoint[] Luxand.CImage.DetectFacialFeaturesInRegion(ref FSDK.TFacePosition FacePosition);
```

**Parameters:**

- **Image** - handle of the image facial features should be detected in.
- **FacePosition** - pointer to the face position structure.
- **FacialFeatures** - pointer to the FSDK_Features array for receiving the detected facial features.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
int i, DetectedCount, img1;
FSDK_Features Features;
TFacePosition FaceArray[50];

FSDK_Initialize("");
FSDK_LoadImageFromFile(&img1, "test.jpg");

FSDK_DetectMultipleFaces(img1, &DetectedCount , FaceArray, sizeof(FaceArray));

for (i = 0; i < DetectedCount; i++) {
    FSDK_DetectFacialFeaturesInRegion(img1, FaceArray[i], Features);
    printf("Left eye location: (%d, %d)\n", Features[FSDKP_LEFT_EYE].x, Features[FSDKP_LEFT_EYE].y);
    printf("Right eye location: (%d, %d)\n", Features[FSDKP_RIGHT_EYE].x, Features[FSDKP_RIGHT_EYE].y);
}
```

**Python Syntax:**

```python
def FSDK.DetectFacialFeaturesInRegion(image: Image, facePosition: FacePosition) -> Features;

def Image.DetectFacialFeatures(image: Image, facePosition: FacePosition = None, *, confidenceLevels = False) -> Features;
```

**Return Value:**

The Features objects.

**Python Example:**

```python
from fsdk import FSDK

FSDK.Initialize()
image = FSDK.Image("test.jpg")

for fpos in image.DetectMultipleFaces():
    features = image.DetectFacialFeatures(image, fpos, confidenceLevel = True)
    print("Left eye location:", features[FSDK.FSDKP_LEFT_EYE], "confidence =", features.confidenceLevels[FSDK.FSDKP_LEFT_EYE])
    print("Right eye location:", features[FSDK.FSDKP_RIGHT_EYE], "confidence =", features.confidenceLevels[FSDK.FSDKP_RIGHT_EYE])
```

<a id="fsdk_detecteyes-function"></a>
## FSDK_DetectEyes Function

Detects a frontal face in an image and detects its eye centers.

**C++ Syntax:**

```cpp
int FSDK_DetectEyes(HImage Image, FSDK_Features* FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectEyes(Image: HImage; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectEyes(int Image, out FSDK.TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.DetectEyes(HImage Image, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.DetectEyes(HImage Image, FSDK_Features FacialFeatures);
```

**CImage Syntax:**

```csharp
FSDK.TPoint[] Luxand.CImage.DetectEyes();
```

**Parameters:**

- **Image** - handle of the image eye centers should be detected in.
- **FacialFeatures** - pointer to the FSDK_Features array for receiving the detected eye centers.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
class Eyes(Point*2):
    """ An array of two 2D coordinates for eyes """

def FSDK.DetectEyes(image: Image) -> Eyes:

def Image.DetectEyes(facePosition: FacePosition = None) -> Eyes;
```

**Return Value:**

The Eyes object.

<a id="fsdk_detecteyesinregion-function"></a>
## FSDK_DetectEyesInRegion Function

Detects eye centers in an image region returned by FSDK_DetectFace or FSDK_DetectMultipleFaces.

**C++ Syntax:**

```cpp
int FSDK_DetectEyesInRegion(HImage Image, TFacePosition* FacePosition, FSDK_Features* FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_DetectEyesInRegion(Image: HImage; FacePosition: PFacePosition; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.DetectEyesInRegion(int Image, ref FSDK.TFacePosition FacePosition, out FSDK.TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.DetectEyesInRegion(HImage Image, TFacePosition FacePosition, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.DetectEyesInRegion(HImage Image, TFacePosition FacePosition, FSDK_Features FacialFeatures);
```

**CImage Syntax:**

```csharp
FSDK.TPoint[] Luxand.CImage.DetectEyesInRegion(ref FSDK.TFacePosition FacePosition);
```

**Parameters:**

- **Image** - handle of the image eye centers should be detected in.
- **FacePosition** - pointer to the face position structure.
- **FacialFeatures** - pointer to the FSDK_Features array for receiving the detected eye centers.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.DetectEyesInRegion(image: Image, facePosition: FacePosition) -> Eyes:

def Image.DetectEyes(facePosition: FacePosition = None) -> Eyes;
```

**Return Value:**

The Eyes object.

<a id="detected-facial-features"></a>
# Detected Facial Features

Luxand FaceSDK detects 70 facial feature points. These facial feature points can be accessed by their names in the FSDK_Features array.

![Detected Features](https://www.luxand.com/facesdk/documentation/images/detected_features_70.jpg)

<a id="facial-feature-points-reference"></a>
## Facial Feature Points Reference

| Facial Feature Name | Value |
|---------------------|-------|
| FSDKP_LEFT_EYE | 0 |
| FSDKP_RIGHT_EYE | 1 |
| FSDKP_LEFT_EYE_INNER_CORNER | 24 |
| FSDKP_LEFT_EYE_OUTER_CORNER | 23 |
| FSDKP_LEFT_EYE_LOWER_LINE1 | 38 |
| FSDKP_LEFT_EYE_LOWER_LINE2 | 27 |
| FSDKP_LEFT_EYE_LOWER_LINE3 | 37 |
| FSDKP_LEFT_EYE_UPPER_LINE1 | 35 |
| FSDKP_LEFT_EYE_UPPER_LINE2 | 28 |
| FSDKP_LEFT_EYE_UPPER_LINE3 | 36 |
| FSDKP_LEFT_EYE_LEFT_IRIS_CORNER | 29 |
| FSDKP_LEFT_EYE_RIGHT_IRIS_CORNER | 30 |
| FSDKP_RIGHT_EYE_INNER_CORNER | 25 |
| FSDKP_RIGHT_EYE_OUTER_CORNER | 26 |
| FSDKP_RIGHT_EYE_LOWER_LINE1 | 41 |
| FSDKP_RIGHT_EYE_LOWER_LINE2 | 31 |
| FSDKP_RIGHT_EYE_LOWER_LINE3 | 42 |
| FSDKP_RIGHT_EYE_UPPER_LINE1 | 40 |
| FSDKP_RIGHT_EYE_UPPER_LINE2 | 32 |
| FSDKP_RIGHT_EYE_UPPER_LINE3 | 39 |
| FSDKP_RIGHT_EYE_LEFT_IRIS_CORNER | 33 |
| FSDKP_RIGHT_EYE_RIGHT_IRIS_CORNER | 34 |
| FSDKP_LEFT_EYEBROW_INNER_CORNER | 13 |
| FSDKP_LEFT_EYEBROW_MIDDLE | 16 |
| FSDKP_LEFT_EYEBROW_MIDDLE_LEFT | 18 |
| FSDKP_LEFT_EYEBROW_MIDDLE_RIGHT | 19 |
| FSDKP_LEFT_EYEBROW_OUTER_CORNER | 12 |
| FSDKP_RIGHT_EYEBROW_INNER_CORNER | 14 |
| FSDKP_RIGHT_EYEBROW_MIDDLE | 17 |
| FSDKP_RIGHT_EYEBROW_MIDDLE_LEFT | 20 |
| FSDKP_RIGHT_EYEBROW_MIDDLE_RIGHT | 21 |
| FSDKP_RIGHT_EYEBROW_OUTER_CORNER | 15 |
| FSDKP_NOSE_TIP | 2 |
| FSDKP_NOSE_BOTTOM | 49 |
| FSDKP_NOSE_BRIDGE | 22 |
| FSDKP_NOSE_LEFT_WING | 43 |
| FSDKP_NOSE_LEFT_WING_OUTER | 45 |
| FSDKP_NOSE_LEFT_WING_LOWER | 47 |
| FSDKP_NOSE_RIGHT_WING | 44 |
| FSDKP_NOSE_RIGHT_WING_OUTER | 46 |
| FSDKP_NOSE_RIGHT_WING_LOWER | 48 |
| FSDKP_MOUTH_RIGHT_CORNER | 3 |
| FSDKP_MOUTH_LEFT_CORNER | 4 |
| FSDKP_MOUTH_TOP | 54 |
| FSDKP_MOUTH_TOP_INNER | 61 |
| FSDKP_MOUTH_BOTTOM | 55 |
| FSDKP_MOUTH_BOTTOM_INNER | 64 |
| FSDKP_MOUTH_LEFT_TOP | 56 |
| FSDKP_MOUTH_LEFT_TOP_INNER | 60 |
| FSDKP_MOUTH_RIGHT_TOP | 57 |
| FSDKP_MOUTH_RIGHT_TOP_INNER | 62 |
| FSDKP_MOUTH_LEFT_BOTTOM | 58 |
| FSDKP_MOUTH_LEFT_BOTTOM_INNER | 63 |
| FSDKP_MOUTH_RIGHT_BOTTOM | 59 |
| FSDKP_MOUTH_RIGHT_BOTTOM_INNER | 65 |
| FSDKP_NASOLABIAL_FOLD_LEFT_UPPER | 50 |
| FSDKP_NASOLABIAL_FOLD_LEFT_LOWER | 52 |
| FSDKP_NASOLABIAL_FOLD_RIGHT_UPPER | 51 |
| FSDKP_NASOLABIAL_FOLD_RIGHT_LOWER | 53 |
| FSDKP_CHIN_BOTTOM | 11 |
| FSDKP_CHIN_LEFT | 9 |
| FSDKP_CHIN_RIGHT | 10 |
| FSDKP_FACE_CONTOUR1 | 7 |
| FSDKP_FACE_CONTOUR2 | 5 |
| FSDKP_FACE_CONTOUR12 | 6 |
| FSDKP_FACE_CONTOUR13 | 8 |
| FSDKP_FACE_CONTOUR14 | 66 |
| FSDKP_FACE_CONTOUR15 | 67 |
| FSDKP_FACE_CONTOUR16 | 68 |
| FSDKP_FACE_CONTOUR17 | 69 |

<a id="mask-on-face-detection"></a>
# Mask-on Face Detection

To detect faces covered by masks, you need to adjust the settings of several parameters. You also need to download a model file trained specifically on masked faces (for visual face detection) and put it into the working directory of your application:

[https://luxand.com/download/fd_masks1.bin](https://luxand.com/download/fd_masks1.bin)

<a id="using-fsdk_detectface-or-fsdk_detectmultiplefaces"></a>
## Using FSDK_DetectFace or FSDK_DetectMultipleFaces

If you are using FSDK_DetectFace or FSDK_DetectMultipleFaces to detect faces (i.e. you don't use Tracker API), use the following code to set the recommended face detection parameters and use the latest model file:

```cpp
int err = 0;
FSDK_SetFaceDetectionParameters(true, false, 1024);
FSDK_SetFaceDetectionThreshold(5);

if (FSDKE_OK !=
    FSDK_SetParameters("FaceDetectionModel=fd_masks1.bin;TrimFacesWithUncertainFacialFeatures=false",
    &err))
{
    fprintf(stderr, "Error loading face detection model!\n");
    exit(3);
}
```

<a id="using-tracker-api"></a>
## Using Tracker API

Alternatively, if you are using Tracker API, use the following calls:

```cpp
int err = 0;
FSDK_SetTrackerMultipleParameters(tracker, "RecognizeFaces=false; HandleArbitraryRotations=true;
    DetermineFaceRotationAngle=false; InternalResizeWidth=1024; FaceDetectionThreshold=5;", &err);

if (FSDKE_OK != FSDK_SetTrackerMultipleParameters(tracker,
    "FaceDetectionModel=fd_masks1.bin;TrimFacesWithUncertainFacialFeatures=false",
    &err))
{
    fprintf(stderr, "Error loading face detection model!\n");
    exit(3);
}
```

<a id="important-notes"></a>
## Important Notes

In the code above, the `TrimFacesWithUncertainFacialFeatures` parameter is set to false. When it is set to true, faces with uncertain facial features are removed from the detection result. As masks may cover many facial features, this setting was preventing such faces from being detected. You can learn more about this parameter in the [Configuration](#facesdk-parameters) section.

We don't recommend that you use face matching when this parameter is set to false, since it will give a higher amount of false acceptances. We plan to update our face recognition models so they support mask-on face matching soon.

We recommend setting the `InternalResizeWidth` parameter to 1024 so the faces that are far from the camera are detected. If you don't expect your faces to be that far, you can lower the parameter value to 512 or 256 to increase the speed of detection.

<a id="face-matching"></a>
# Face Matching

Luxand FaceSDK provides the API to extract face templates and match them. A template extracted from a face can be stored in a database and can then be used to match faces using the [FSDK_MatchFaces](#fsdk_matchfaces-function) function.

To extract a face template, use the [FSDK_GetFaceTemplate](#fsdk_getfacetemplate-function), [FSDK_GetFaceTemplateInRegion](#fsdk_getfacetemplateinregion-function) or FSDK_GetFaceTemplateUsingFeatures functions. The [FSDK_MatchFaces](#fsdk_matchfaces-function) function returns the facial similarity level. You may consider similarity to be equal to the probability that templates belong to the same person.

*More precisely: if the access control system provides access to a person when similarity is higher of threshold x, the possibility of providing erroneous access to another person is 1-x. For example, if the decision to provide access to a person is based on the code*

```cpp
if (similarity > 0.99)
   AllowAccess();
```

*the possibility of erroneous access to another person is 0.01, or 1%.*

A facial template contains data that describes the face. There is no direct way to re-create the original face image from a template. However, when using Tracker API, it may store the original facial images in Tracker memory (see the Storing original facial images section).

To determine if the matched templates belong to the same person (with a specified error possibility), you can compare the facial similarity value with a threshold calculated by the [FSDK_GetMatchingThresholdAtFAR](#fsdk_getmatchingthresholdatfar-function) or [FSDK_GetMatchingThresholdAtFRR](#fsdk_getmatchingthresholdatfrr-function) functions.

Note: it is recommended to retain both the original face images and their templates in the database. This is because future versions of Luxand FaceSDK may offer an improved template extraction algorithm, together with changes to the template format. If you are using Tracker API, there is an option to convert its memory automatically if the template format changes (see the Storing original facial images section).

A face template is stored in the FSDK_FaceTemplate data structure.

In .NET, there is no specific data type for a template. Instead, it is stored in an array of bytes of FSDK.TemplateSize length. Below is an example of retrieving facial template in C#.

**C# Example:**

```csharp
templateData = new byte[FSDK.TemplateSize];
FSDK.GetFaceTemplate(imageHandle, out templateData);
```

**C++ Declaration:**

```cpp
typedef struct {
    char ftemplate [1040];
} FSDK_FaceTemplate;
```

**Delphi Declaration:**

```pascal
FSDK_FaceTemplate = record
    Template: array[0.. 1040-1] of byte;
end;
PFSDK_FaceTemplate = ^FSDK_FaceTemplate;
```

**Java and Android Declaration:**

The class FSDK_FaceTemplate has the following property:

```java
FSDK_FaceTemplate = record
    public byte template[];
```

**Python Declaration:**

```python
FSDK.FaceTemplate = c_char*const.FSDK_FACE_TEMPLATE_SIZE
```

<a id="fsdk_getfacetemplate-function"></a>
## FSDK_GetFaceTemplate Function

This function is used to extract a template from a facial image. The function first detects a face, then detects its facial features and extracts the template.

If there is more than one face in the image, the template is extracted for the face with the most clearly visible details. If there is no clearly visible face, the function returns an error code. To set the threshold determining the accepted quality for faces, use the FSDK_SetFaceDetectionThreshold function.

If the face position or its features or eye centers are known, it is more efficient to use the [FSDK_GetFaceTemplateInRegion](#fsdk_getfacetemplateinregion-function) or [FSDK_GetFaceTemplateUsingEyes](#fsdk_getfacetemplateusingeyes-function) functions. To extract the template for a specific face, use the [FSDK_GetFaceTemplateInRegion](#fsdk_getfacetemplateinregion-function) function.

**C++ Syntax:**

```cpp
int FSDK_GetFaceTemplate(HImage Image, FSDK_FaceTemplate* FaceTemplate);
```

**Delphi Syntax:**

```pascal
function FSDK_GetFaceTemplate(Image: HImage; FaceTemplate: PFSDK_FaceTemplate): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetFaceTemplate(int Image, out byte[] FaceTemplate);
```

**Java Syntax:**

```java
int FSDK.GetFaceTemplate(HImage Image, FSDK_FaceTemplate.ByReference FaceTemplate);
```

**Android Syntax:**

```java
int FSDK.GetFaceTemplate(HImage Image, FSDK_FaceTemplate FaceTemplate);
```

**CImage Syntax:**

```csharp
byte[] Luxand.CImage.GetFaceTemplate();
```

**Parameters:**

*Image* - handle of the image from which to extract the face template.

*FaceTemplate* - pointer to the FSDK_FaceTemplate structure, used to receive the face template.

**Return Value:**

Returns FSDKE_OK if successful. If no faces are found, or the quality of the image is not sufficient, the function returns the FSDKE_FACE_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.GetFaceTemplate(image: Image) -> FaceTemplate;

def Image.GetFaceTemplate(facePosition: FacePosition = None) -> FaceTemplate;
```

**Return Value:**

The FaceTemplate object.

<a id="fsdk_getfacetemplateinregion-function"></a>
## FSDK_GetFaceTemplateInRegion Function

Extracts a template for a face located in a specific region returned by FSDK_DetectFace or FSDK_DetectMultipleFaces.

The function detects facial features in a specific region and extracts a template. The face detection stage is not performed. This function can be useful if an approximate face size and position is known, or to process a specific face returned by FSDK_DetectFace or FSDK_DetectMultipleFaces. The function returns no error if the face is not clearly visible. This is because it assumes that if face detection functions return a detected face position, the face is of sufficient quality.

If facial features or eye centers are known, it is more efficient to use the [FSDK_GetFaceTemplateUsingFeatures](#fsdk_getfacetemplateusingfeatures-function) or [FSDK_GetFaceTemplateUsingEyes](#fsdk_getfacetemplateusingeyes-function) function.

**C++ Syntax:**

```cpp
int FSDK_GetFaceTemplateInRegion(HImage Image, TFacePosition* FacePosition, FSDK_FaceTemplate* FaceTemplate);
```

**Delphi Syntax:**

```pascal
function FSDK_GetFaceTemplateInRegion(Image: HImage; FacePosition: PFacePosition; FaceTemplate: PFSDK_FaceTemplate): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetFaceTemplateInRegion(int Image, ref FSDK.TFacePosition FacePosition, out byte[] FaceTemplate);
```

**Java Syntax:**

```java
int FSDK.GetFaceTemplateInRegion(HImage Image, TFacePosition FacePosition, FSDK_FaceTemplate.ByReference FaceTemplate);
```

**Android Syntax:**

```java
int FSDK.GetFaceTemplateInRegion(HImage Image, TFacePosition FacePosition, FSDK_FaceTemplate FaceTemplate);
```

**CImage Syntax:**

```csharp
byte[] Luxand.CImage.GetFaceTemplateInRegion(ref FSDK.TFacePosition FacePosition);
```

**Parameters:**

*Image* - handle of the image from which to extract the face template.

*FacePosition* - pointer to the face position structure.

*FaceTemplate* - pointer to the FSDK_FaceTemplate structure, used to receive the face template.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetFaceTemplate(image: Image, facePosition: FacePosition) -> FaceTemplate;

def Image.GetFaceTemplate(facePosition: FacePosition = None) -> FaceTemplate;
```

**Return Value:**

The FaceTemplate object.

<a id="fsdk_getfacetemplateusingeyes-function"></a>
## FSDK_GetFaceTemplateUsingEyes Function

Extracts a face template using the detected eye centers.

The function receives eye centers coordinates detected by the FSDK_DetectFacialFeatures, FSDK_DetectFacialFeaturesInRegion, FSDK_DetectEyes or FSDK_DetectEyesInRegion functions and extracts a face template. Face detection, facial feature detection, and eye centers detection are not performed. This function can be useful when facial features or eye centers for a specific face are already detected. The function returns no error if the face is not clearly visible, since it assumes that if the face and its facial features or eye centers are already detected, the face is of sufficient quality.

Note that the FSDK_GetFaceTemplate, FSDK_GetFaceTemplateInRegion and FSDK_GetFaceTemplateUsingFeatures functions return templates that could be matched with higher accuracy, so it is recommended to use these functions instead.

**C++ Syntax:**

```cpp
int FSDK_GetFaceTemplateUsingEyes(HImage Image, FSDK_Features* eyeCoords, FSDK_FaceTemplate* FaceTemplate);
```

**Delphi Syntax:**

```pascal
function FSDK_ GetFaceTemplateUsingEyes(Image: HImage; eyeCoords: PFSDK_Features; FaceTemplate: PFSDK_FaceTemplate): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetFaceTemplateUsingEyes(int Image, ref FSDK.TPoint[] eyeCoords, out byte[] FaceTemplate);
```

**Java Syntax:**

```java
int FSDK.GetFaceTemplateUsingEyes(HImage Image, FSDK_Features eyeCoords, FSDK_FaceTemplate.ByReference FaceTemplate);
```

**Android Syntax:**

```java
int FSDK.GetFaceTemplateUsingEyes(HImage Image, FSDK_Features eyeCoords, FSDK_FaceTemplate FaceTemplate);
```

**CImage Syntax:**

```csharp
byte[] Luxand.CImage.GetFaceTemplateUsingEyes(ref FSDK.TPoint[] eyeCoords);
```

**Parameters:**

*Image* - handle of the image to extract the face template from.

*eyeCoords* - pointer to the FSDK_Features array containing eye centers coordinates.

*FaceTemplate* - pointer to the FSDK_FaceTemplate structure for receiving the face template.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetFaceTemplateUsingEyes(image: Image, eyesCoord: Eyes) -> FaceTemplate;
```

**Return Value:**

The FaceTemplate object.

<a id="fsdk_getfacetemplateusingfeatures-function"></a>
## FSDK_GetFaceTemplateUsingFeatures Function

Extracts a face template using the detected facial feature coordinates.

The function receives facial feature coordinates detected by the FSDK_DetectFacialFeatures or FSDK_DetectFacialFeaturesInRegion functions and extracts a face template. Face detection, facial feature detection, and eye centers detection are not performed. This function can be useful when facial features for a specific face are already detected. The function produces no error if the face is not clearly visible, since it assumes that if the face and its facial features are already detected, the face is of sufficient quality.

The function determines if facial features, starting with the 2nd, are equal to zero or uninitialized. In this case, the functions calls [FSDK_GetFaceTemplateUsingEyes](#fsdk_getfacetemplateusingeyes-function) instead.

**C++ Syntax:**

```cpp
int FSDK_GetFaceTemplateUsingFeatures(HImage Image, FSDK_Features* FacialFeatures, FSDK_FaceTemplate* FaceTemplate);
```

**Delphi Syntax:**

```pascal
function FSDK_ GetFaceTemplateUsingFeatures(Image: HImage; FacialFeatures: PFSDK_Features; FaceTemplate: PFSDK_FaceTemplate): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetFaceTemplateUsingFeatures(int Image, ref FSDK.TPoint[]FacialFeatures, out byte[] FaceTemplate);
```

**Java Syntax:**

```java
int FSDK.GetFaceTemplateUsingFeatures(HImage Image, FSDK_Features FacialFeatures, FSDK_FaceTemplate.ByReference FaceTemplate);
```

**Android Syntax:**

```java
int FSDK.GetFaceTemplateUsingFeatures(HImage Image, FSDK_Features FacialFeatures, FSDK_FaceTemplate FaceTemplate);
```

**CImage Syntax:**

```csharp
byte[] Luxand.CImage.GetFaceTemplateUsingFeatures(ref FSDK.TPoint[]FacialFeatures);
```

**Parameters:**

*Image* - handle of the image to extract the face template from.

*FacialFeatures* - pointer to the FSDK_Features array containing facial feature coordinates.

*FaceTemplate* - pointer to the FSDK_FaceTemplate structure for receiving the face template.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetFaceTemplateUsingFeatures(image: Image, facialFeatures: FacialFeatures) -> FaceTemplate;
```

**Return Value:**

The FaceTemplate object.

<a id="fsdk_matchfaces-function"></a>
## FSDK_MatchFaces Function

Match two face templates. The returned value determines the similarity of the faces.

**C++ Syntax:**

```cpp
int FSDK_MatchFaces(FSDK_FaceTemplate* FaceTemplate1, FSDK_FaceTemplate* FaceTemplate2, float* Similarity);
```

**Delphi Syntax:**

```pascal
function FSDK_MatchFaces(FaceTemplate1, FaceTemplate2: PFSDK_FaceTemplate; Similarity: PSingle): integer;
```

**C# Syntax:**

```csharp
int FSDK.MatchFaces(ref byte[] FaceTemplate1, ref byte[] FaceTemplate2, ref float Similarity);
```

**Java Syntax:**

```java
int FSDK.MatchFaces(FSDK_FaceTemplate.ByReference FaceTemplate1, FSDK_FaceTemplate.ByReference FaceTemplate2, float Similarity[]);
```

**Android Syntax:**

```java
int FSDK.MatchFaces(FSDK_FaceTemplate FaceTemplate1, FSDK_FaceTemplate FaceTemplate2, float Similarity[]);
```

**Parameters:**

*FaceTemplate1* - pointer to the FSDK_FaceTemplate structure, using the first template for comparison.

*FaceTemplate2* - pointer to the FSDK_FaceTemplate structure, using the second template for comparison.

*Similarity* - pointer to a float value, used to receive the similarity of the face templates.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INVALID_TEMPLATE if any of the face templates is in an invalid format.

Returns FSDKE_UNSUPPORTED_TEMPLATE_VERSION if any of the templates is created with an unsupported version of FaceSDK.

**Python Syntax:**

```python
def FSDK.MatchFaces(faceTemplate1: FaceTemplate, faceTemplate2: FaceTemplate) -> float;

def FaceTemplate.MatchFaces(faceTemplate: FaceTemplate) -> float;
```

**Return Value:**

The similarity of the face templates.

<a id="fsdk_getmatchingthresholdatfar-function"></a>
## FSDK_GetMatchingThresholdAtFAR Function

This function returns the threshold value for similarity to determine if two matched templates belong to the same person at a given FAR (False Acceptance Rate) value. The FAR determines the acceptable error rate when two different people's templates are mistakenly recognized as the same person. Decreasing FAR leads to an increase in FRR - i.e. with low FAR it becomes more probable that two templates from the same person will be determined as belonging to different people.

**C++ Syntax:**

```cpp
int FSDK_GetMatchingThresholdAtFAR(float FARValue, float* Threshold);
```

**Delphi Syntax:**

```pascal
function FSDK_GetMatchingThresholdAtFAR(FARValue: single; var Threshold: single): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetMatchingThresholdAtFAR(float FARValue, ref float Threshold);
```

**Java and Android Syntax:**

```java
int FSDK.GetMatchingThresholdAtFAR(float FARValue, float Threshold[]);
```

**Parameters:**

*FARValue* - the desired FAR value. Varies from 0.0 (means 0%) to 1.0 (means 100%).

*Threshold* - pointer to a float variable to store the calculated Threshold value.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
FSDK_FaceTemplate template1, template2;

float MatchingThreshold, Similarity;
FSDK_GetMatchingThresholdAtFAR(0.02, &MatchingThreshold);

FSDK_GetFaceTemplate(img1, &template1);
FSDK_GetFaceTemplate(img2, &template2);
FSDK_MatchFaces(&template1, &template2, &Similarity);
if (Similarity > MatchingThreshold)
   printf("Same Person\n");
else
   printf("Different Person\n");
```

**Python Syntax:**

```python
def FSDK.GetMatchingThresholdAtFAR(FRRValue: float) -> float;
```

**Return Value:**

The calculated Threshold value.

<a id="fsdk_getmatchingthresholdatfrr-function"></a>
## FSDK_GetMatchingThresholdAtFRR Function

This function returns the threshold value for similarity to determine if two matched templates belong to the same person at a given FRR (False Rejection Rate) value. The FRR determines the acceptable error rate when two templates of the same person are identified as belonging to different people. Decreasing FRR leads to an increase in FAR - i.e. with low FRR it becomes more probable that two different people's templates will be recognized as the same person.

**C++ Syntax:**

```cpp
int FSDK_GetMatchingThresholdAtFRR(float FRRValue, float* Threshold);
```

**Delphi Syntax:**

```pascal
function FSDK_GetMatchingThresholdAtFRR(FRRValue: single; var Threshold: single): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetMatchingThresholdAtFRR(float FRRValue, ref float Threshold);
```

**Java and Android Syntax:**

```java
int FSDK.GetMatchingThresholdAtFRR(float FRRValue, float Threshold[]);
```

**Parameters:**

*FRRValue* - the desired FRR value. Varies from 0.0 (means 0%) to 1.0 (means 100%).

*Threshold* - pointer to a float variable, used to store the calculated Threshold value.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetMatchingThresholdAtFRR(FRRValue: float) -> float;
```

**Return Value:**

The calculated Threshold value.

---

<a id="managing-recognition-thresholds-for-identity-verification"></a>
## Managing Recognition Thresholds for Identity Verification

In a critical identity verification system, choosing the right threshold is essential for balancing security (minimizing false positives) against usability (minimizing false negatives).

<a id="understanding-far-and-frr"></a>
### Understanding FAR and FRR

- **FAR (False Acceptance Rate)** — the probability of incorrectly accepting an impostor as a genuine user. Lower FAR means higher security.
- **FRR (False Rejection Rate)** — the probability of incorrectly rejecting a genuine user. Lower FRR means better usability.

FAR and FRR are inversely related: decreasing one increases the other. The optimal threshold depends on your application's security requirements.

<a id="choosing-the-right-threshold"></a>
### Choosing the Right Threshold

| Use Case | Recommended FAR | Security Level |
|---|---|---|
| High-security access control | 0.001 (0.1%) | Very strict — few false accepts, more false rejects |
| Standard identity verification | 0.01 (1%) | Balanced — good security with acceptable usability |
| Convenience-focused unlock | 0.05 (5%) | Permissive — minimal false rejects, higher false accept risk |

<a id="complete-threshold-management-example-c"></a>
### Complete Threshold Management Example (C++)

```cpp
// Initialize and activate the SDK
FSDK_Initialize("");
FSDK_ActivateLibrary("your-license-key-here");

// Identity verification with configurable threshold
int err;
float threshold;
float similarity;
FSDK_FaceTemplate enrolledTemplate, probeTemplate;

// Set threshold based on security requirements
// For high-security: FAR = 0.001 (0.1% false acceptance)
err = FSDK_GetMatchingThresholdAtFAR(0.001f, &threshold);
if (err != FSDKE_OK) {
    printf("Error getting threshold: %d\n", err);
    return;
}

// Extract templates from both images
err = FSDK_GetFaceTemplate(enrolledImage, &enrolledTemplate);
if (err != FSDKE_OK) {
    printf("Error: could not extract template from enrolled image (error %d)\n", err);
    return;
}

err = FSDK_GetFaceTemplate(probeImage, &probeTemplate);
if (err != FSDKE_OK) {
    printf("Error: could not extract template from probe image (error %d)\n", err);
    return;
}

// Match faces and compare against threshold
err = FSDK_MatchFaces(&enrolledTemplate, &probeTemplate, &similarity);
if (err != FSDKE_OK) {
    if (err == FSDKE_INVALID_TEMPLATE)
        printf("Error: invalid face template\n");
    else if (err == FSDKE_UNSUPPORTED_TEMPLATE_VERSION)
        printf("Error: template version mismatch\n");
    return;
}

// Make verification decision
if (similarity >= threshold) {
    printf("MATCH: Same person (similarity=%.4f, threshold=%.4f)\n", similarity, threshold);
} else {
    printf("NO MATCH: Different person (similarity=%.4f, threshold=%.4f)\n", similarity, threshold);
}
```

<a id="complete-threshold-management-example-python"></a>
### Complete Threshold Management Example (Python)

```python
from fsdk import FSDK

# Initialize and activate the SDK
FSDK.Initialize()
FSDK.ActivateLibrary("your-license-key-here")

# Get threshold for desired security level
threshold = FSDK.GetMatchingThresholdAtFAR(0.01)  # 1% false acceptance rate

# Load images and extract templates
try:
    img1 = FSDK.Image("enrolled.jpg")
    template1 = img1.GetFaceTemplate()
except FSDK.FaceNotFound:
    print("Error: no face detected in enrolled image")
    exit(1)

try:
    img2 = FSDK.Image("probe.jpg")
    template2 = img2.GetFaceTemplate()
except FSDK.FaceNotFound:
    print("Error: no face detected in probe image")
    FSDK.FreeImage(img1)
    exit(1)

# Compare faces
similarity = FSDK.MatchFaces(template1, template2)

# Verification decision with confidence reporting
if similarity >= threshold:
    print(f"VERIFIED: similarity={similarity:.4f} >= threshold={threshold:.4f}")
else:
    print(f"REJECTED: similarity={similarity:.4f} < threshold={threshold:.4f}")

# Clean up
FSDK.FreeImage(img1)
FSDK.FreeImage(img2)
```

<a id="handling-false-positives-and-false-negatives"></a>
### Handling False Positives and False Negatives

**To reduce false positives (impostors accepted):**
- Use a lower FAR value (e.g., 0.001 instead of 0.01)
- Require multiple verification attempts and accept only if all pass
- Combine face recognition with other authentication factors

**To reduce false negatives (genuine users rejected):**
- Use a higher FAR value if security requirements allow
- Ensure enrollment images are high quality with good lighting and frontal pose
- Store multiple templates per person taken under different conditions
- Retry with a new probe image before final rejection

**Monitoring in production:**
- Log all similarity scores to detect threshold drift over time
- Track FAR and FRR rates against expected values
- Re-enroll users whose rejection rate increases (appearance may have changed)

<a id="gender-age-and-facial-expression-recognition"></a>
# Gender, Age and Facial Expression Recognition

The SDK recognizes the gender, age and facial expressions of subjects. It recognizes if a smile is present and if the eyes are open or closed. To accomplish this, first you must detect facial features in an image, and then pass these features to the [FSDK_DetectFacialAttributeUsingFeatures](#fsdk_detectfacialattributeusingfeatures-function) function, specifying the *"Gender"*, the *"Age"* or the *"Expression"* attribute.

<a id="fsdk_detectfacialattributeusingfeatures-function"></a>
## FSDK_DetectFacialAttributeUsingFeatures Function

Detects an attribute of a face, and returns the Values of a particular attribute, and Confidences in these Values.

Each facial attribute has a number of Values, and each Value has an associated Confidence. A Value is a string, and a Confidence is a float from 0 to 1, which represents confidence level of this particular value of the attribute.

The following attribute names are supported:

*"Liveness"* - to get the liveness probability (see the [Passive Liveness](#passive-liveness) section).

*"Gender"* - to detect the gender of a face. The attribute has *"Male"* and *"Female"* values.

*"Age"* - to detect the age of a face. The attribute has *"Age"* value.

*"Expression"* - to detect the expression of a face. The attribute has *"Smile"* and *"EyesOpen"* values.

The Values and their Confidences are returned in a string of the following format:

`"Value1=Confidence1[;Value2=Confidence2[;...]]"`

For example, when calling the function with the *"Gender"* attribute, the following string may be returned:

`"Male=0.95721;Female=0.04279"`

It means that the subject has male gender with a confidence of 95.7%, and female gender with a confidence of 4.3%.

When calling the function with the *"Age"* attribute, the following string may be returned:

`"Age=37"`

When calling the function with the *"Expression"* attribute, the following string may be returned:

`"Smile=0.987;EyesOpen=0.9952"`

It means that the subject smiles with a confidence of 98.7%, and the eyes are open with a confidence of 99.5%.

You may use several attributes in a single function call separated by ";". For example, if AttributeName is *"Gender; Age; Expression"*, the result may be the following: `"Male=0.95721;Female=0.04279;Age=37;Smile=0.987;EyesOpen=0.9952"`.

You may use the [FSDK_GetValueConfidence](#fsdk_getvalueconfidence-function) to parse the returned string and retrieve the Confidences for individual Values.

**C++ Syntax:**

```cpp
int FSDK_DetectFacialAttributeUsingFeatures(HImage Image, const FSDK_Features * FacialFeatures, const char * AttributeName, char * AttributeValues, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```delphi
function FSDK_DetectFacialAttributeUsingFeatures(Image: HImage; FacialFeatures: PFSDK_Features; AttributeName, AttributeValues: PAnsiChar; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int DetectFacialAttributeUsingFeatures(int Image, ref TPoint [] FacialFeatures, string AttributeName, out string AttributeValues, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.DetectFacialAttributeUsingFeatures(int Image, FSDK_Features FacialFeatures, String AttributeName, String AttributeValues[], long MaxSizeInBytes);
```

**Parameters:**

*Image* - HImage handle in which to detect the attribute.

*FacialFeatures* - pointer to the FSDK_Features array containing facial feature coordinates.

*AttributeName* - name of the attribute. You may specify several attributes separated by ";".

*AttributeValues* - pointer to the null-terminated string that will receive the attribute Names and their Confidences.

*MaxSizeInBytes* - amount of memory allocated for the output string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.DetectFacialAttributeUsingFeatures(image: Image, facialFeatures: Features, attributeName: str, ret_dict: bool = False) -> str

def Image.DetectFacialAttributeUsingFeatures(facialFeatures: Features, attributeName: str, ret_dict: bool = False) -> str
```

**Return Value:**

If ret_dict is False (default) the return value is a string object with the attribute Names and their Confidence.
If ret_dict is True the return value is a dict object with the attribute Names as keys and Confidence floats as values.

---

<a id="fsdk_getvalueconfidence-function"></a>
## FSDK_GetValueConfidence Function

Parses the string returned by [FSDK_DetectFacialAttributeUsingFeatures](#fsdk_detectfacialattributeusingfeatures-function) or [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function), and returns the Confidence in an individual Value.

**C++ Syntax:**

```cpp
int FSDK_GetValueConfidence(const char * AttributeValues, const char * Value, float * Confidence);
```

**Delphi Syntax:**

```delphi
function FSDK_GetValueConfidence(AttributeValues, Value: PAnsiChar; Confidence: PSingle): integer;
```

**C# Syntax:**

```csharp
int GetValueConfidence(string AttributeValues, string Value, ref float Confidence);
```

**Java and Android Syntax:**

```java
int FSDK.GetValueConfidence(String AttributeValues, String Value, float Confidence[]);
```

**Parameters:**

*AttributeValues* - pointer to the null-terminated string containing the attribute Values and their Confidences.

*Value* - pointer to the null-terminated string containing the desired Value.

*Confidence* - pointer to the float variable to store the Confidence in a Value.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
char AttributeValues[1024];
FSDK_DetectFacialAttributeUsingFeatures(image, features, "Gender", AttributeValues, sizeof(AttributeValues));
float ConfidenceMale = 0.0f;
float ConfidenceFemale = 0.0f;
FSDK_GetValueConfidence(AttributeValues, "Male", &ConfidenceMale);
FSDK_GetValueConfidence(AttributeValues, "Female", &ConfidenceFemale);
```

**Python Syntax:**

```python
def FSDK.GetValueConfidence(attributeValues: str, value: str) -> float
```

**Return Value:**

The Confidence value.
Use DetectFacialAttributeUsingFeatures function with *ret_dict* argument set to True to get a dict object with Confidence float values.

---

<a id="complete-attribute-detection-workflow"></a>
## Complete Attribute Detection Workflow

To extract gender, age, and expression from a face, you must first initialize the library, load an image, detect facial features, and then call the attribute detection function. Below are complete working examples with error handling.

<a id="complete-example-c"></a>
### Complete Example (C++)

```cpp
#include "LuxandFaceSDK.h"
#include <cstdio>

int main() {
    // Step 1: Initialize FaceSDK
    int err = FSDK_Initialize("");
    if (err != FSDKE_OK) {
        printf("Failed to initialize FaceSDK (error %d)\n", err);
        return 1;
    }

    // Step 2: Activate with your license key
    err = FSDK_ActivateLibrary("your-license-key-here");
    if (err != FSDKE_OK) {
        printf("Failed to activate FaceSDK (error %d)\n", err);
        return 1;
    }

    // Step 3: Load image
    HImage image;
    err = FSDK_LoadImageFromFile(&image, "photo.jpg");
    if (err != FSDKE_OK) {
        printf("Failed to load image (error %d)\n", err);
        return 1;
    }

    // Step 4: Detect facial features
    FSDK_Features features;
    err = FSDK_DetectFacialFeatures(image, &features);
    if (err != FSDKE_OK) {
        printf("No face detected (error %d)\n", err);
        FSDK_FreeImage(image);
        return 1;
    }

    // Step 5: Detect all attributes in a single call
    char attrValues[1024];
    err = FSDK_DetectFacialAttributeUsingFeatures(image, &features,
        "Gender;Age;Expression", attrValues, sizeof(attrValues));
    if (err != FSDKE_OK) {
        printf("Attribute detection failed (error %d)\n", err);
        FSDK_FreeImage(image);
        return 1;
    }

    // Step 6: Parse results
    float confMale, confFemale, confSmile, confEyesOpen;
    FSDK_GetValueConfidence(attrValues, "Male", &confMale);
    FSDK_GetValueConfidence(attrValues, "Female", &confFemale);
    FSDK_GetValueConfidence(attrValues, "Smile", &confSmile);
    FSDK_GetValueConfidence(attrValues, "EyesOpen", &confEyesOpen);

    // Determine gender (use 0.5 threshold)
    printf("Gender: %s (confidence: %.1f%%)\n",
        confMale > confFemale ? "Male" : "Female",
        (confMale > confFemale ? confMale : confFemale) * 100.0);

    // Parse age from the raw string (format: "...;Age=37;...")
    float age;
    FSDK_GetValueConfidence(attrValues, "Age", &age);
    printf("Age: %.0f\n", age);

    // Expression (smile confidence > 0.5 means smiling)
    printf("Smiling: %s (confidence: %.1f%%)\n",
        confSmile > 0.5 ? "Yes" : "No", confSmile * 100.0);
    printf("Eyes open: %s (confidence: %.1f%%)\n",
        confEyesOpen > 0.5 ? "Yes" : "No", confEyesOpen * 100.0);

    // Cleanup
    FSDK_FreeImage(image);
    return 0;
}
```

<a id="complete-example-python"></a>
### Complete Example (Python)

```python
from fsdk import FSDK

# Initialize and activate
FSDK.Initialize()
FSDK.ActivateLibrary("your-license-key-here")

# Load image and detect features
image = FSDK.LoadImageFromFile("photo.jpg")
features = image.DetectFacialFeatures()

# Detect all attributes at once, get results as a dictionary
attrs = image.DetectFacialAttributeUsingFeatures(
    features, "Gender;Age;Expression", ret_dict=True
)

# Parse results
gender = "Male" if attrs["Male"] > 0.5 else "Female"
gender_conf = attrs["Male"] if attrs["Male"] > 0.5 else attrs["Female"]
print(f"Gender: {gender} (confidence: {gender_conf:.1%})")
print(f"Age: {attrs['Age']:.0f}")
print(f"Smiling: {'Yes' if attrs['Smile'] > 0.5 else 'No'} ({attrs['Smile']:.1%})")
print(f"Eyes open: {'Yes' if attrs['EyesOpen'] > 0.5 else 'No'} ({attrs['EyesOpen']:.1%})")

# Cleanup
FSDK.FreeImage(image)
```

<a id="interpreting-confidence-values"></a>
### Interpreting Confidence Values

- **Gender**: `Male` and `Female` confidences sum to 1.0. Use a threshold of **0.5** to determine the predicted gender.
- **Age**: The `Age` value is an estimated integer age, not a confidence score.
- **Smile**: A confidence above **0.5** indicates the subject is likely smiling. Values above 0.9 indicate a clear smile.
- **EyesOpen**: A confidence above **0.5** indicates the eyes are likely open. Use this for blink detection by monitoring changes across frames.

<a id="liveness-detection"></a>
# Liveness Detection

The SDK offers several approaches to detect spoofing attempts (when a photo or a video is presented to the camera instead of a real person). There are [passive liveness detection](#passive-liveness), [active liveness detection](#active-liveness), and [thermal face detection](#thermal-face-detection). A combination of several approaches provides the best reliability.

The SDK provides enhanced passive liveness detection.

<a id="passive-liveness"></a>
## Passive Liveness

Passive liveness detection is the most sophisticated anti-spoofing technology. It does not require any special hardware, nor does it ask users to perform any actions to prove the liveness - it works just by analyzing images.

Passive liveness detection works with both still images and videos. The probability of a subject being live is available as the `Liveness` facial attribute. For still images, the attribute can be retrieved with the [FSDK_DetectFacialAttributeUsingFeatures](#fsdk_detectfacialattributeusingfeatures-function) function. For videos, use the [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function) function of Tracker API. To enable passive liveness detection in Tracker API, make sure to pass the `"DetectLiveness=true"` parameter to Tracker API.

Using Tracker API for passive liveness detection usually improves the reliability of the liveness detection, as liveness is detected in a number of facial appearances on consecutive video frames. The resulting liveness probability *p* is calculated as a soft minimum:

![Liveness Formula](https://www.luxand.com/facesdk/documentation/images/liveness_formula.png)

where *p<sub>i</sub>* is the liveness probability detected on the frame *i*; *n* is the number of frames.

The following Tracker parameters can be used to adjust passive liveness detection:

`AttributeLivenessSmoothingAlpha` - the *О±* parameter. The default value is 1.

`LivenessFramesCount` - the minimum number of frames required before the liveness attribute is calculated. The default value is 15.

Note that an RGB color image is required to perform the passive liveness check, grayscale images aren't supported.

<a id="active-liveness"></a>
## Active Liveness

Active liveness check requires Tracker API, as demonstrated in the [ActiveLiveness samples](#sample-applications). Liveness is verified by asking the user to perform a set of actions in front of the camera.

<a id="thermal-face-detection"></a>
## Thermal Face Detection

Thermal face detection can also be used to verify liveness. In a typical scenario, the system is equipped with a thermal camera and an ordinary "visual" camera. Both cameras should capture the same field of view. To ensure a face is live, it must be detected in the same place both by the visual and the thermal camera. For more information see the [Face Detection on Thermal Images](#face-detection-on-thermal-images) section.

<a id="ibeta-certified-liveness-add-on"></a>
# iBeta Certified Liveness Add-on

Available for Linux, Windows (x64), Android and iOS.

iBeta certified Liveness add-on for FaceSDK passed Level 1 iBeta Presentation Attack Detection (PAD) conformance testing with a perfect PAD score. iBeta Quality Assurance conducted Presentation Attack Detection (PAD) testing in accordance with ISO/IEC 30107-3. iBeta is accredited by NIST/NVLAP (NVLAP Lab Code: 200962) to test and provide results to this PAD standard.

[View the iBeta Lab confirmation letter with the assessment results](https://www.ibeta.com/wp-content/uploads/2024/01/240105-Luxand-PAD-Level-1-Confirmation-Letter.pdf)

During the evaluation, iBeta researchers conducted about a thousand presentation attacks using subjects' authentic biometric samples to create artifacts. None of these presentation attacks were successful, resulting in an Attack Presentation Classification Error Rate (APCER) of 0%.

As a uniquely accredited third-party biometrics testing lab, iBeta Quality Assurance ensures that products meet the highest standards of functionality and security. The iBeta certification guarantees the most precise liveness and anti-spoofing checks for images and videos.

Sample projects are available at https://www.luxand.com/facesdk/download/.

---

<a id="activation"></a>
## Activation

iBeta liveness add-on requires a license key, which should be installed on the target Windows, or Linux system before starting your application.

If the key is not present you will be unable to use the iBeta add-on. The license key is a file with the .v2c extension, you can find it in the sample's license directory. To install it, run the install_license utility that is bundled along with the key: **install_license *.v2c**

---

<a id="initialization"></a>
## Initialization

To initialize the iBeta add-on you should call the following function:

```cpp
int res = FSDK_SetParameter("LivenessModel", "external");
```

The returned value should be equal to `FSDKE_OK`. Ensure that the data directory is in the application's working directory. If not, you can set it as follows:

```cpp
int res = FSDK_SetParameter("LivenessModel", "external:dataDir=" + dataDirectory);
```

**Possible returned error codes:**

| Error Code | Description |
|------------|-------------|
| `FSDKE_PLUGIN_NO_PERMISSION` | You don't have permission to use the iBeta add-on (e.g., incorrect FaceSDK license key type) |
| `FSDKE_PLUGIN_NOT_LOADED` | Something went wrong during the add-on loading. Ensure that all necessary files are available and exist in the application's working directory. |

---

<a id="general-usage"></a>
## General Usage

To check liveness on an image, load the image using the FSDK_LoadImageFromFile function, detect facial features, and then obtain the liveness attribute using these features. Below is a code sample in C++:

```cpp
HImage img;
FSDK_Features features;
char attributes[512];
float liveness = 0.0f;
float image_quality = 0.0f;
const char* image = "image.png";

FSDK_LoadImageFromFile(&img, image);
FSDK_DetectFacialFeatures(img, &features);
FSDK_DetectFacialAttributeUsingFeatures(img, &features, "Liveness", attributes, 512);
FSDK_GetValueConfidence(attributes, "Liveness", &liveness);
FSDK_GetValueConfidence(attributes, "ImageQuality", &image_quality);
```

Note that you should check the returning values of every function.

The main factor in determining whether the image is live or spoofed is the liveness value (probability). An image can be considered live if the liveness value is higher than 0.5. An additional factor to consider is the image_quality value, which measures how "appropriate" the image is for the liveness check. Images with quality values lower than 0.5 should generally be rejected. Both measurements are float values in the range of [0, 1].

Sometimes an image may be rejected. If this happens, you can get a liveness check error message in the attributes variable after the "LivenessError=" prefix. An example of error parsing in C++:

```cpp
string e = "LivenessError=";
if (string(attributes).find(e) != string::npos) {
    string livenessErrorMessage = string(attributes).substr(e.length());
}
```

<a id="using-tracker-api"></a>
### Using Tracker API

When using the Tracker API with the iBeta add-on, you should set the following parameters:

```cpp
FSDK_SetTrackerParameter(tracker, "DetectLiveness", "true");
FSDK_SetTrackerParameter(tracker, "SmoothAttributeLiveness", "false");
FSDK_SetTrackerParameter(tracker, "AttributeLivenessSmoothingAlpha", "1");
FSDK_SetTrackerParameter(tracker, "LivenessFramesCount", "1");
```

Sample code in C++ for Tracker API:

```cpp
HImage image;
char attributes[1024];
char err[1024];
float liveness = 0.0f;
float image_quality = 0.0f;
std::string e = "LivenessError=";

while (!is_finished) {
    FSDK_FeedFrame(tracker, camera, image, &count, ids, 256 * sizeof(long long));
    FSDK_GetTrackerFacialAttribute(tracker, camera, ids[0], "Liveness", attributes, 1024);
    FSDK_GetValueConfidence(attributes, "Liveness", &liveness);
    FSDK_GetValueConfidence(attributes, "ImageQuality", &image_quality);
    FSDK_GetTrackerFacialAttribute(tracker, camera, ids[0], "LivenessError", err, 1024);

    string livenessError = string(err).substr(e.length());
}
```

---

<a id="ibeta-liveness-add-on-files"></a>
## iBeta Liveness Add-on Files

To use the iBeta add-on, ensure that all necessary files are in the application's working directory. Below is a list of required files and directories for the supported platforms:

<a id="windows"></a>
### Windows

```text
data
facesdk.dll
IBetaPlugin.dll
idliveface.dll
openvino.dll
openvino_intel_cpu_plugin.dll
openvino_ir_frontend.dll
tbb12.dll
plugins.xml
```

<a id="linux"></a>
### Linux

```text
data
libtbb.so.X
libopenvino.so.X
libopenvino_ir_frontend.so.X
libopenvino_onnx_frontend.so.X
libfsdk.so
libIBetaPlugin.so
libidliveface.so
libopenvino_intel_cpu_plugin.so
plugins.xml
```

<a id="android"></a>
### Android

```text
app/src/main/assets/data
app/src/main/libs/external.jar
app/src/main/jniLibs/arm64-v8a/libfsdk.so
app/src/main/jniLibs/arm64-v8a/libIBetaPlugin.so
app/src/main/jniLibs/arm64-v8a/libidliveface.so
app/src/main/jniLibs/arm64-v8a/libtensorflowlite_c.so

(same file structure for armeabi-v7a and x86_64)
```

<a id="ios"></a>
### iOS

```text
FaceSDK/data
FaceSDK/FaceSdk.framework
FaceSDK/fsdk.framework
FaceSDK/IBetaPlugin.framework
FaceSDK/LuxandFaceSDK.h
```

---

<a id="image-requirements"></a>
## Image Requirements

<a id="image-format"></a>
### Image Format

Lossless formats are preferred, as lossy compression can negatively affect accuracy. If you use lossy formats, make sure the compression is at a minimal level. For example, for JPEG, 70 is the lowest practical compression level.

<a id="image-resolution"></a>
### Image Resolution

The iBeta Liveness add-on processes the area around the face, so the optimal resolution will depend on the image composition. Assuming a portrait orientation with the face centered and occupying at least 1/4 of the image area, the recommended image resolution range is from 600x800 to 960x1280.

<a id="image-composition"></a>
### Image Composition

- There should be only one main face in the image. It should be fully visible within the frame, fully open, and without any occlusions. Cropping is not allowed. Small faces in the background are not taken into account.
- The minimum size of a face box that can be processed is 150x150 pixels.
- The padding between the face box and the image's borders should be at least 15 pixels.
- The distance between the pupils on the face should be at least 50 pixels.
- The out-of-plane rotation angle (face pitch and yaw) should be no more than В±30 degrees.

Images that do not meet these conditions will be rejected. Other factors that can affect accuracy include:

- Motion blur can significantly increase BPCER (the rate of errors classifying a genuine person as a spoof).
- Texture filtering can significantly increase APCER (the rate of errors allowing impostors through).
- Spotlights on the face and nearby surroundings can significantly increase BPCER.
- Poorly lit environments and colored lighting can significantly increase BPCER.
- Fish-eye lenses are not supported.
- Sunglasses may cause confusion.

---

<a id="sample-images"></a>
## Sample Images

This section contains image samples categorized into three groups:

- Good samples: Images with optimal face size, positioning, and lighting conditions.
- Acceptable but suboptimal samples: Images that are acceptable but were taken under less-than-ideal conditions.
- Incorrect samples: Images that are not acceptable for processing.

<a id="good-examples"></a>
### Good Examples

![Good Example 1](https://www.luxand.com/facesdk/documentation/images/good_example_1.png) ![Good Example 2](https://www.luxand.com/facesdk/documentation/images/good_example_2.png)

<a id="correct-but-not-good-enough-samples"></a>
### Correct, But Not Good Enough Samples

**A distance between the camera and the face is too great:**

![Distance Too Great](https://www.luxand.com/facesdk/documentation/images/distance_between_the_camera_too_great.png)

**The face is partially obscured by headwear:**

![Face Partially Obscured](https://www.luxand.com/facesdk/documentation/images/face_is_partially_obscured.png)

<a id="incorrect-samples"></a>
### Incorrect Samples

**Poor lighting conditions:**

![Poor Lighting](https://www.luxand.com/facesdk/documentation/images/poor_lighting_conditions.png)

**Headwear obscures the face too much:**

![Obscures Too Much](https://www.luxand.com/facesdk/documentation/images/obscures_the_face_too_much.png)

**Incorrect head rotation:**

![Incorrect Rotation](https://www.luxand.com/facesdk/documentation/images/incorrect_head_rotation.png)

**The face is too close to the camera:**

![Face Too Close](https://www.luxand.com/facesdk/documentation/images/face_is_too_close.png)

**The face is positioned incorrectly, partially out of frame:**

![Partially Out of Frame](https://www.luxand.com/facesdk/documentation/images/face_partially_out_of_frame.png)

---

<a id="configuration-files"></a>
## Configuration Files

It is possible to change internal parameters used to validate the image. Lower values will result in fewer images being rejected, but accuracy may degrade for such images. The parameters are defined in the **data/preprocessing/face_params.conf** file.

Available parameters:

| Parameter | Description | Default |
|-----------|-------------|---------|
| `min_face_size` | Minimum width and height of the face box, in pixels | 150 |
| `min_face_size_relative` | Minimum relative width and height of the face box, as a ratio of the face's width and height to the image's width and height. Value between 0 and 1. | 0.15 |
| `detectable_face_size_relative` | Similar to above, but if the size of the face box is smaller than this value, the face is simply skipped. Used as a filter for small faces in the background. | 0.075 |
| `min_pupillary_distance` | Minimum distance between the pupils on the face, in pixels | 50 |
| `min_face_padding` | Minimum distance from the image's border to the face box, in pixels | 15 |
| `max_roll` | Maximum roll angle of the head, in degrees | 45 |
| `max_yaw` | Maximum yaw angle of the head, in degrees | 30 |
| `max_pitch` | Maximum pitch angle of the head, in degrees | 30 |

<a id="working-with-cameras"></a>
# Working with Cameras

The library offers a set of functions to work with DirectShow/v4l2-compatible web cameras and IP cameras with an MJPEG interface. The functions allow single frames to be retrieved from a camera one-by-one; they are stored in HImage descriptors. The application usually grabs frames in a loop, displaying each frame in its window and performing manipulations with images (such as face detection).

Web camera functions are available only for Windows and Linux platforms. IP camera functions are available for all platforms.

Android and iOS samples include platform-specific code working with cameras on phones and tablets.

<a id="data-types"></a>
## Data Types

There are data types to store the information about video formats. Note that the names of video cameras are stored in wide char format (each char occupies two bytes).

**C++ Declaration:**

```cpp
typedef struct {
    int Width;
    int Height;
    int BPP;
} FSDK_VideoFormatInfo;

typedef enum {
    FSDK_MJPEG
} FSDK_VIDEOCOMPRESSIONTYPE;
```

**C# Declaration:**

```csharp
public struct VideoFormatInfo
{
   public int Width;
   public int Height;
   public int BPP;
}
```

**Delphi Declaration:**

```pascal
FSDK_VideoFormatInfo = record
   Width: integer;
   Height: integer;
   BPP: integer;
end;

PFSDK_VideoFormatInfo = ^FSDK_VideoFormatInfo;
FSDK_VideoFormatInfoArray = array[0..255] of FSDK_VideoFormatInfo;
PFSDK_VideoFormatInfoArray = ^FSDK_VideoFormatInfoArray;
FSDK_CameraList = array[0..255] of PWideChar;
PFSDK_CameraList = ^FSDK_CameraList;
FSDK_VIDEOCOMPRESSIONTYPE = ( FSDK_MJPEG );
```

**Java Declaration:**

```java
The class FSDK_VideoFormatInfo has the following properties:

   public int Width, Height, BPP;

class FSDK_VideoFormats {
   public FSDK_VideoFormatInfo.ByValue formats[];
}

class TCameras {
   public String cameras[];
}
```

**Java and Android Declaration:**

```java
class HCamera {
   protected int hcamera;
}

class FSDK_VIDEOCOMPRESSIONTYPE {
   public static final int FSDK_MJPEG = 0;
}
```

**Python Declaration:**

```python
class Camera(ctypes.Structure):
    fields_ = ("handle", c_int),  # FSDK camera handle
    def __init__(self, cameraName=None):  # cameraName is for windows only
    def Open(self, cameraName);
    def Close(self)
    def GrabFrame(self)

# for windows and linux only
class VideoFormatInfo(ctypes.Structure):
    fields = ("Width", c_int), ("Height", c_int), ("FormatIndex", c_int)
```

<a id="fsdk_initializecapturing-function"></a>
## FSDK_InitializeCapturing Function

This function initializes the capturing process (but does not open a camera). This function should be called in a certain thread that works with cameras. Note that on Windows platforms this function initializes COM in the thread; if you already initialized COM, you must not call this function, and you must not call [FSDK_FinalizeCapturing](#fsdk_finalizecapturing-function).

**C++ Syntax:**

```cpp
int FSDK_InitializeCapturing(void);
```

**Delphi Syntax:**

```pascal
function FSDK_InitializeCapturing: integer;
```

**C# Syntax:**

```csharp
int FSDKCam.InitializeCapturing();
```

**Java Syntax:**

```java
int FSDKCam.InitializeCapturing();
```

**Android Syntax:**

```java
int FSDK.InitializeCapturing();
```

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.InitializeCapturing();
```

**Return Value:**

None

<a id="fsdk_finalizecapturing-function"></a>
## FSDK_FinalizeCapturing Function

This function finalizes the capturing process, initialized by the [FSDK_InitializeCapturing](#fsdk_initializecapturing-function) function (and finalizes COM on Windows platforms). If you already finalized COM, you must not call this function.

**C++ Syntax:**

```cpp
int FSDK_FinalizeCapturing(void);
```

**Delphi Syntax:**

```pascal
function FSDK_FinalizeCapturing: integer;
```

**C# Syntax:**

```csharp
int FSDKCam.FinalizeCapturing();
```

**Java Syntax:**

```java
int FSDKCam.FinalizeCapturing();
```

**Android Syntax:**

```java
int FSDK.FinalizeCapturing();
```

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.FinalizeCapturing();
```

**Return Value:**

None.

<a id="fsdk_setcameranaming-function"></a>
## FSDK_SetCameraNaming Function

Sets the retrieval format for the [FSDK_GetCameraList](#fsdk_getcameralist-function) function. Depending on the value of the argument, either web camera names (by default) or their unique IDs (Device Path) are returned. Device Path may be necessary if the system has several web cameras from the same manufacturer that have the same name. This function does not support IP cameras.

**C++ Syntax:**

```cpp
int FSDK_SetCameraNaming(bool UseDevicePathAsName);
```

**Delphi Syntax:**

```pascal
function FSDK_SetCameraNaming(UseDevicePathAsName: boolean): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.SetCameraNaming(bool UseDevicePathAsName)
```

**Java Syntax:**

```java
int FSDKCam.SetCameraNaming (boolean UseDevicePathAsName);
```

**Parameters:**

*UseDevicePathAsName* - sets a retrieval format for the [FSDK_GetCameraList](#fsdk_getcameralist-function) function.

**FALSE:** [FSDK_GetCameraList](#fsdk_getcameralist-function) returns the list of names for cameras installed in the system;

**TRUE:** [FSDK_GetCameraList](#fsdk_getcameralist-function) returns the list of unique device paths of these cameras.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetCameraNaming(useDevicePathAsName: bool):
```

**Return Value:**

None.

<a id="fsdk_getcameralist-function"></a>
## FSDK_GetCameraList Function

This function retrieves the list of web cameras available in the system. The name of each camera is stored in wide char format (each character occupies two bytes). The function does not support IP cameras. The camera list must be destroyed by calling the [FSDK_FreeCameraList](#fsdk_freecameralist-function) function after the list is no longer needed.

**C++ Syntax:**

```cpp
int FSDK_GetCameraList(wchar_t*** CameraList, int* CameraCount);
```

**Delphi Syntax:**

```pascal
function FSDK_GetCameraList(CameraList: PWideChar; CameraCount: Pinteger): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.GetCameraList(out string[] CameraList, out int CameraCount)
```

**Java Syntax:**

```java
int FSDKCam.GetCameraList(TCameras CameraList, int CameraCount[]);
```

**Parameters:**

*CameraList* - pointer to wchar_t** variable to store the camera list.

*CameraCount* - pointer to integer variable to store the count of cameras in the system.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
wchar_t** CameraList;
int CameraCount;

FSDK_InitializeCapturing();
if (FSDK_GetCameraList(&CameraList, &CameraCount)==FSDKE_OK)
    for (int i=0; i<CameraCount; i++)
        wprintf(L"camera: %s\n", CameraList[i]);
printf("%d camera(s) found.\n", CameraCount);
FSDK_FinalizeCapturing();
```

**Python Syntax:**

```python
class CameraName(str);

def FSDK.ListCameraNames() -> List[CameraName];
```

**Return Value:**

The list of CameraName objects.

**Note:**

The CameraName class is a string with an extra field *devicePath*.

<a id="fsdk_getcameralistex-function"></a>
## FSDK_GetCameraListEx Function

This function retrieves the list of names and the device paths of the web cameras available in the system. The name and the device path of each camera are stored in wide char format (each character occupies two bytes) at the same indices at the corresponding arrays. The function does not support IP cameras. Both lists must be destroyed by calling the [FSDK_FreeCameraList](#fsdk_freecameralist-function) function after they are no longer needed.

**C++ Syntax:**

```cpp
int FSDK_GetCameraListEx(wchar_t*** CameraNameList, wchar_t*** CameraDevicePathList, int* CameraCount);
```

**Delphi Syntax:**

```pascal
function FSDK_GetCameraListEx(CameraNameList: PWideChar; CameraDevicePathList: PWideChar; CameraCount: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.GetCameraList(out string[] CameraNameList, out string[] CameraDevicePathList, out int CameraCount)
```

**Java Syntax:**

```java
int FSDKCam.GetCameraListEx(TCameras CameraNameList, TCameras CameraDevicePathList, int CameraCount[]);
```

**Parameters:**

*CameraNameList* - pointer to wchar_t** variable to store the camera name list.

*CameraDevicePathList* - pointer to wchar_t** variable to store the camera device path list.

*CameraCount* - pointer to integer variable to store the number of cameras in the system.

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdk_freecameralist-function"></a>
## FSDK_FreeCameraList Function

This function frees the list of web cameras obtained from the [FSDK_GetCameraList](#fsdk_getcameralist-function) or [FSDK_GetCameraListEx](#fsdk_getcameralistex-function) function. The call of the function is not required in .NET, VB and Java.

**C++ Syntax:**

```cpp
int FSDK_FreeCameraList(wchar_t*** CameraList, int CameraCount);
```

**Delphi Syntax:**

```pascal
function FSDK_FreeCameraList(CameraList: Pointer; CameraCount: integer): integer;
```

**Parameters:**

*CameraList* - pointer to wchar_t** variable where the camera list is stored.

*CameraCount* - the count of cameras in the system, obtained from the [FSDK_GetCameraList](#fsdk_getcameralist-function) or [FSDK_GetCameraListEx](#fsdk_getcameralistex-function) function.

**Note:**

You must call [FSDK_FreeCameraList](#fsdk_freecameralist-function) for *CameraNameList* and *CameraDevicePathList*, if you were using [FSDK_GetCameraListEx](#fsdk_getcameralistex-function).

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdk_getvideoformatlist-function"></a>
## FSDK_GetVideoFormatList Function

This function returns the list of video formats supported by a given camera. This function does not support IP cameras.

**C++ Syntax:**

```cpp
int FSDK_GetVideoFormatList(wchar_t* CameraName, FSDK_VideoFormatInfo** VideoFormatList, int* VideoFormatCount);
```

**Delphi Syntax:**

```pascal
function FSDK_GetVideoFormatList(CameraName: PWideChar; VideoFormatList: PFSDK_VideoFormatInfo; VideoFormatCount: Pinteger): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.GetVideoFormatList(string CameraName, out FSDKcam.VideoFormatInfo[] VideoFormatList, out int VideoFormatCount)
```

**Java Syntax:**

```java
int FSDKCam.GetVideoFormatList(String CameraName, FSDK_VideoFormats VideoFormatList, int VideoFormatCount[]);
```

**Parameters:**

*CameraName* - pointer to name of desired video camera.

*VideoFormatList* - pointer to FSDK_VideoFormatInfo* variable to store the list of video formats.

*VideoFormatCount* - pointer to integer variable to store the count of video formats.

**Return Value:**

Returns FSDKE_OK if successful.

<a id="fsdk_freevideoformatlist-function"></a>
## FSDK_FreeVideoFormatList Function

This function frees the list of video formats obtained from [FSDK_GetVideoFormatList](#fsdk_getvideoformatlist-function). Calling this function is not required in .NET, VB and Java.

**C++ Syntax:**

```cpp
int FSDK_FreeVideoFormatList(FSDK_VideoFormatInfo * VideoFormatList);
```

**Delphi Syntax:**

```pascal
function FSDK_FreeVideoFormatList(VideoFormatList: Pointer): integer;
```

**Parameters:**

*VideoFormatList* - pointer to FSDK_VideoFormatInfo* variable where the list of video formats is stored.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.ListVideoFormats(cameraName: str) -> List[VideoFormatInfo];
```

**Return Value:**

The list of VideoFormatInfo objects.

<a id="fsdk_setvideoformat-function"></a>
## FSDK_SetVideoFormat Function

The function sets the format of camera output. The function does not support IP cameras.

**C++ Syntax:**

```cpp
int FSDK_SetVideoFormat(wchar_t* CameraName, FSDK_VideoFormatInfo VideoFormat);
```

**Delphi Syntax:**

```pascal
function FSDK_SetVideoFormat(CameraName: PWideChar; VideoFormat: FSDK_VideoFormatInfo): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.SetVideoFormat(ref string CameraName, FSDKcam.VideoFormatInfo VideoFormat);
```

**Java Syntax:**

```java
int FSDKCam.SetVideoFormat(String CameraName, FSDK_VideoFormatInfo.ByValue VideoFormat);
```

**Parameters:**

*CameraName* - pointer to name of desired video camera.

*VideoFormat* - desired video format.

**Return Value:**

Returns FSDKE_OK if successful.

**Example:**

```cpp
wchar_t** CameraList;
int CameraCount;
FSDK_VideoFormatInfo* VideoFormatList;
int VideoFormatCount;

FSDK_GetCameraList(&CameraList, &CameraCount);

FSDK_GetVideoFormatList(CameraList[0], &VideoFormatList, &VideoFormatCount);
FSDK_SetVideoFormat(CameraList[0], VideoFormatList[0]);
```

**Python Syntax:**

```python
def FSDK.SetVideoFormat(cameraName: str, videoFormat: VideoFormatInfo);
```

**Return Value:**

None.

<a id="fsdk_openvideocamera-function"></a>
## FSDK_OpenVideoCamera Function

The function opens the web camera of a given name and returns its handle.

**C++ Syntax:**

```cpp
int FSDK_OpenVideoCamera(wchar_t* CameraName, int* CameraHandle);
```

**Delphi Syntax:**

```pascal
function FSDK_OpenVideoCamera(CameraName: PWideChar; CameraHandle: Pinteger): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.OpenVideoCamera(ref string CameraName, ref int CameraHandle);
```

**Java Syntax:**

```java
int FSDKCam.OpenVideoCamera (String CameraName, HCamera CameraHandle);
```

**Parameters:**

*CameraName* - pointer to name of web camera to open.

*CameraHandle* - pointer to integer variable to store the opened camera handle.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.OpenVideoCamera(cameraName: str) -> Camera;
```

**Return Value:**

New Camera object.

<a id="fsdk_openipvideocamera-function"></a>
## FSDK_OpenIPVideoCamera Function

This function opens the IP camera at a given URL and returns its handle. You may call the [FSDK_SetHTTPProxy](#fsdk_sethttpproxy-function) function to set an HTTP proxy for accessing the camera.

**C++ Syntax:**

```cpp
int FSDK_OpenIPVideoCamera(FSDK_VIDEOCOMPRESSIONTYPE CompressionType, char * URL, char * Username, char * Password, int TimeoutSeconds, int * CameraHandle);
```

**Delphi Syntax:**

```pascal
function FSDK_OpenIPVideoCamera(CompressionType: FSDK_VIDEOCOMPRESSIONTYPE; URL: PAnsiChar; Username: PAnsiChar; Password: PAnsiChar; TimeoutSeconds: integer; CameraHandle: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.OpenIPVideoCamera(FSDK_VIDEOCOMPRESSIONTYPE CompressionType, string URL, string Username, string Password, int TimeoutSeconds, ref int CameraHandle);
```

**Java Syntax:**

```java
int FSDKCam.OpenIPVideoCamera(int CompressionType, String URL, String Username, String Password, int TimeoutSeconds, HCamera CameraHandle);
```

**Android Syntax:**

```java
int FSDK.OpenIPVideoCamera(FSDK_VIDEOCOMPRESSIONTYPE CompressionType, String URL, String Username, String Password, int TimeoutSeconds, HCamera CameraHandle);
```

**Parameters:**

*CompressionType* - the type of video stream (MJPEG by default).

*URL* - URL of the IP camera to be opened.

*Username* - IP camera access username.

*Password* - IP camera access password.

*TimeoutSeconds* - connection timeout in seconds.

*CameraHandle* - pointer to integer variable to store the opened camera handle.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.OpenIPVideoCamera(compression: int, URL: str, userName: str, password: str, timeoutSeconds: int) -> Camera;
```

**Return Value:**

New Camera object.

<a id="fsdk_sethttpproxy-function"></a>
## FSDK_SetHTTPProxy Function

This function sets an HTTP proxy to be used with an IP camera. If a proxy is required, the function should be called before the [FSDK_OpenIPVideoCamera](#fsdk_openipvideocamera-function) function.

**C++ Syntax:**

```cpp
int FSDK_SetHTTPProxy(char* ServerNameOrIPAddress, unsigned short Port, char* UserName, char* Password);
```

**Delphi Syntax:**

```pascal
function FSDK_SetHTTPProxy(ServerNameOrIPAddress: PAnsiChar; Port: Word; Username: PAnsiChar; Password: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetHTTPProxy(string ServerNameOrIPAddress, UInt16 Port, string UserName, string Password);
```

**Java Syntax:**

```java
int FSDKCam.SetHTTPProxy(String ServerNameOrIPAddress, int Port, String UserName, String Password);
```

**Android Syntax:**

```java
int FSDK.SetHTTPProxy(String ServerNameOrIPAddress, short Port, String UserName, String Password);
```

**Parameters:**

*ServerNameOrIPAddress* - proxy address.

*Port* - proxy port.

*UserName* - proxy username.

*Password* - proxy password.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetHTTPProxy(serverNameOrIPAddress: str, port: int, userName: str, password: str);
```

**Return Value:**

None.

<a id="fsdk_grabframe-function"></a>
## FSDK_GrabFrame Function

Retrieves the current frame from a web camera or an IP camera and stores the frame in the created HImage handle. If a camera returns an image, mirrored horizontally (it depends on the camera settings), then you can mirror it by using [FSDK_MirrorImage](#fsdk_mirrorimage-function).

**C++ Syntax:**

```cpp
int FSDK_GrabFrame(int CameraHandle, HImage* Image);
```

**Delphi Syntax:**

```pascal
function FSDK_GrabFrame(CameraHandle: integer; var Image: PHImage): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.GrabFrame(int CameraHandle, ref int Image);
```

**Java Syntax:**

```java
int FSDKCam.GrabFrame(HCamera CameraHandle, HImage Image);
```

**Android Syntax:**

```java
int FSDK.GrabFrame(HCamera CameraHandle, HImage Image);
```

**Parameters:**

*CameraHandle* - handle of the opened camera to grab frame.

*Image* - pointer to HImage variable to store the frame. Note that the created HImage handle should be deleted once it is no longer needed using the [FSDK_FreeImage](#fsdk_freeimage-function) function.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GrabFrame(camera: Camera) -> Image;

def Camera.GrabFrame() -> Image;
```

**Return Value:**

A new image with grabbed frame.

<a id="fsdk_closevideocamera-function"></a>
## FSDK_CloseVideoCamera Function

This function closes the camera, opened by the [FSDK_OpenVideoCamera](#fsdk_openvideocamera-function) or [FSDK_OpenIPVideoCamera](#fsdk_openipvideocamera-function) function.

**C++ Syntax:**

```cpp
int FSDK_CloseVideoCamera(int CameraHandle);
```

**Delphi Syntax:**

```pascal
function FSDK_CloseVideoCamera(CameraHandle: integer): integer;
```

**C# Syntax:**

```csharp
int FSDKCam.CloseVideoCamera(int CameraHandle);
```

**Java Syntax:**

```java
int FSDKCam.CloseVideoCamera(HCamera CameraHandle);
```

**Parameters:**

*CameraHandle* - handle of opened video camera to close.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CloseVideoCamera(camera: Camera);

def Camera.Close();
```

**Return Value:**

None.

**Note:**

The camera is closed automatically by calling the destructor of Camera object.

<a id="tracker-api-face-recognition-and-tracking-in-video-streams"></a>
# Tracker API: Face Recognition and Tracking in Video Streams

<a id="what-is-tracker-api"></a>
## What is Tracker API

Tracker API is a set of functions that allows for recognizing subjects in live video streams. The API receives the video frame by frame, and assigns a unique identifier (ID) to each subject detected in the video. Thus, each subject can be determined by its ID across the video. You can attach a name tag to an identifier, and query any identifier for its name. The API also allows simple face tracking (without registering subjects); tracking of the coordinates of either all facial features or just eye centers; and recognition of subjects' gender, age and facial expression. The API provides an estimate of both recognition rate and false acceptance rate as the video progresses.

If your task is to track or recognize faces in video streams, consider using Tracker API instead of manually calling functions like [FSDK_DetectFace](#fsdk_detectface-function), [FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function) or [FSDK_GetFaceTemplate](#fsdk_getfacetemplate-function) for each frame ("manual handling"). The difference between Tracker API and manual handling is summarized in the table below.

<a id="tracker-api-vs-manual-handling"></a>
## Tracker API vs Manual Handling

|  | Tracker API | Manual handling |
|---|---|---|
| **Development effort** | A developer uses a few Tracker API functions to handle an incoming video frame and set and retrieve subjects' names. The API automatically learns the appearance of every detected subject. | A developer must implement different modes in the program: a mode to enroll subjects and a mode to recognize faces. In the enrollment mode, the program must store a certain (usually found experimentally) number of face templates in the database, while the subject is posing in front of the camera. In recognition mode, a template for each detected face is created and is matched against the database. |
| **Performance** | The API constantly learns how subjects appear. Thus, its recognition rate is usually higher than of a system that merely stores several templates of a subject. | If environmental conditions (such as lighting) change after the enrollment, the system may not recognize the subject, and a new enrollment will be required. |
| **Recognition rates** | Tracker API provides the estimate of recognition rate and false acceptance rate specifically for video streams. | [FSDK_MatchFaces](#fsdk_matchfaces-function) provides FAR/FRR values for matching a pair of images. Typically, it is not easy to estimate how the storage of several templates per person affects recognition rate, how often false acceptances occur as the video progresses, and if false acceptance rate increases as more subjects are enrolled. |
| **Enrollment** | The subject is generally not required to pose. When the operator assigns a name to the subject, it is likely that Tracker API has already captured enough views of a subject to recognize it in later frames. | The subject is required to pose in front of the camera, for the system to capture the face in different views and environmental conditions, and with different facial expressions. |
| **Recognition without enrollment** | Every subject is recognized, regardless of whether it was already tagged with a name. The API assigns a unique ID to track the subject across the video. This allows for surveillance applications, when subjects cannot be required to participate willingly (that is, to pose) to be enrolled for recognition. | Only enrolled subjects can be recognized. The requirement to participate actively in recognition makes surveillance applications difficult. |
| **Tracking of multiple faces** | The API tracks, recognizes, and allows assigning names to multiple faces simultaneously present in the video frame. | Usually only a single subject can pose in front of the camera when enrolling. If other subjects are visible, the system may mistakenly store their templates into the subject's database record. A separate tracking mechanism is required to decide whether the detected face belongs to the enrolled subject or not. |
| **Facial feature detection** | Tracker API allows tracking of facial feature coordinates of each subject in the video frame. Jitter is eliminated by smoothing. | The coordinates detected by [FSDK_DetectFacialFeatures](#fsdk_detectfacialfeatures-function) may jitter because of noise present in the video. If multiple faces are present, a tracking mechanism is required to implement smoothing. |
| **Gender and age recognition** | The API allows for identifying gender and age for each subject tracked in the video. The analysis of the video usually provides higher recognition rates than still image gender and age recognition. | When each video frame is treated as a still image, gender and age recognition rates are usually lower. |
| **Facial expression recognition** | The API allows for identifying if a smile is present and if the eyes are open or closed for each subject tracked in the video. The analysis of the video usually provides higher recognition rates than still image expression recognition. | When each video frame is treated as a still image, expression recognition rates are usually lower. |

---

<a id="understanding-identifiers"></a>
## Understanding Identifiers

The API analyzes the video stream sequentially, frame by frame. For each frame, the [FSDK_FeedFrame](#fsdk_feedframe-function) function returns the list of identifiers (integer numbers) of faces recognized in this frame. The purpose of an identifier is to assign a unique number to each subject in the video. If a face is similar to one recognized previously, it receives the same identifier. Otherwise, a new identifier (in ascending numeric order) is assigned. Thus, subjects recognized as different should get different identifiers.

It is important to note that the identifier value is meaningful only within a particular video stream. Identifiers of the same subject are not expected to be the same across different video streams.

<a id="a-subject-can-have-several-identifiers"></a>
### A subject can have several identifiers

The same subject can get different identifiers in different frames (for example, ID1 in the first frame and ID2 in the second, ID2 > ID1), if the system was not able to match its face to ones previously seen (which might happen if the appearance of the subject on the second frame was notably or unexpectedly different).

<a id="merger-of-identifiers"></a>
### Merger of identifiers

However, as the video progresses, the system learns more about the appearance of each person; at some point it may deduce that ID1 and ID2 actually represent the same person. In such a case (and if it is possible) it merges both identifiers into ID1, further returning ID1 for every novel recognized occurrence of this subject. The system retains the information of all merger events, so it is possible to receive the resulting value of an early assigned identifier (for example, receive the ID1 value when providing the ID2 value) by calling the [FSDK_GetIDReassignment](#fsdk_getidreassignment-function) function. Note that if an identifier was tagged with a name, it can be merged only with other identifiers that are untagged; in such a case the tagged name is retained.

When calling Tracker API functions with identifiers received on earlier frames, it is always recommended to convert the identifier values with the [FSDK_GetIDReassignment](#fsdk_getidreassignment-function) function first, and only then pass them to Tracker API. The reason is that they may have been merged on the subsequent frames, so the corresponding subjects are being represented with other identifier values.

<a id="when-identifiers-are-not-merged"></a>
### When identifiers are not merged

The API supports tagging an identifier with a name, provided by the user. If identifiers are tagged with different names, they will not be merged.

The appearances of each subject are stored in the memory (see the Memory section). If a subject has been tagged with a name, and the memory for this subject is full, it will not be merged with any other identifier (because such a merger requires additional memory for the subject).

<a id="similar-identifiers"></a>
### Similar identifiers

The identifier returned by the [FSDK_FeedFrame](#fsdk_feedframe-function) function can be similar enough to other identifiers for the API to decide they represent the same person. Still, some reason (such as the one described above) may prevent them from merging. In such case, similar identifiers of an ID can be retrieved using the [FSDK_GetSimilarIDList](#fsdk_getsimilaridlist-function) function.

You should always retrieve the list of similar identifiers when deciding if the recognized face belongs to a certain subject or not. Let us assume that you have a particular subject of interest and should respond when it is recognized. You may have stored an identifier of that subject, or assigned a name to it with [FSDK_SetName](#fsdk_setname-function), and wait for such identifier (or name) to appear. (Keep in mind that you need to adjust the stored identifier with [FSDK_GetIDReassignment](#fsdk_getidreassignment-function) after calling [FSDK_FeedFrame](#fsdk_feedframe-function).) When the subject appears, however, there is no guarantee that the stored identifier will be returned by the [FSDK_FeedFrame](#fsdk_feedframe-function) function. Instead, it may appear in the list of similar identifiers. Therefore, you should compare your identifier against the list of similar identifiers for each ID returned by [FSDK_FeedFrame](#fsdk_feedframe-function). Accordingly, you need to retrieve the names of each similar identifier, for each ID returned by [FSDK_FeedFrame](#fsdk_feedframe-function), to find if any of these names belong to the subject of interest. If you are not considering such lists of similar identifiers, your recognition rate will be lower (that is, you may miss the appearance of the subject of interest). Of course, your false acceptance rate will be lower as well. But the drop in recognition rate will be higher compared to when you set a higher recognition threshold (see the [Recognition Performance](#recognition-performance) section), and handle similar identifiers.

The function [FSDK_GetAllNames](#fsdk_getallnames-function) implements the above functionality - it returns the name of an identifier, concatenated with the names (if any) of similar identifiers, separated by a semicolon.

---

<a id="tracker-memory"></a>
## Tracker Memory

The API allows limiting the memory used by a tracker. The memory size is measured in the total number of facial appearances stored (about 11 Kbytes per appearance when the *KeepFaceImages* parameter is set to true, and about 1.5 Kbytes when set to false). By default, the limit is 2150 appearances (about 24 Mbytes or 3 Mbytes depending on the value of the *KeepFaceImages* parameter). You can change the limit by setting the *MemoryLimit* parameter (see the [Tracker Parameters](#tracker-parameters) section) to your desired value.

<a id="memory-available-for-each-subject"></a>
### Memory available for each subject

For each subject tagged with a name, the amount of memory available is:

```text
max(1, memoryLimit/(subjectCount+1))
```

where subjectCount is the total number of subjects tagged with a name. The remaining memory is dedicated to untagged identifiers.

If, when setting a name with [FSDK_SetName](#fsdk_setname-function), there is not enough room for a new subject, the API will return the FSDKE_INSUFFICIENT_TRACKER_MEMORY_LIMIT error.

<a id="imposing-memory-limits"></a>
### Imposing memory limits

If a memory limit for an identifier, tagged with a name, is approached, then no new appearances of that subject will be stored. That is, the system stops learning novel appearances of the subject. Furthermore, the identifier will not be merged with any other identifiers.

If a memory limit is approached for untagged identifiers, the earliest untagged facial appearance becomes purged when calling [FSDK_FeedFrame](#fsdk_feedframe-function). Note that only a particular appearance of some untagged identifier becomes purged, not the identifier's entire record of appearances; identifiers that have only one occurrence are purged completely. To prevent purging, you may use the [FSDK_LockID](#fsdk_lockid-function) function.

Note that if an identifier is tagged, and does not occupy more memory than available per subject, its facial appearances are not purged.

<a id="how-to-set-the-memory-limit"></a>
### How to set the memory limit

The higher the limit, the more identifiers you can tag, and the more facial appearances can be stored for each identifier (thus improving the recognition rate). However, the Threshold parameter should also be higher (but setting too high a Threshold has its downsides - see the [Recognition Performance](#recognition-performance) section), for the false acceptance rate to stay at an acceptable level.

When increasing MemoryLimit, the frame rate may decrease. Therefore, it is practical to choose a memory limit that will allow for a sufficient frame rate, will not require too high a threshold, and will consume only a certain amount of memory, while at the same time allowing for the storage of the desired number of subjects.

See the [Recognition Performance](#recognition-performance) section to find which Threshold values should be chosen with different memory limits to achieve the desired recognition rates.

---

<a id="tracker-parameters"></a>
## Tracker Parameters

Each HTracker instance allows setting a number of parameters with the [FSDK_SetTrackerParameter](#fsdk_settrackerparameter-function) or [FSDK_SetTrackerMultipleParameters](#fsdk_settrackermultipleparameters-function) function.

<a id="face-tracking-parameters"></a>
### Face tracking parameters

Note that the Tracker API does not use the parameters of face detection, set with [FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function) or [FSDK_SetFaceDetectionThreshold](#fsdk_setfacedetectionthreshold-function). Instead, you should use the Tracker API parameters below.

- **FaceDetectionModel, TrimOutOfScreenFaces, TrimFacesWithUncertainFacialFeatures** - the parameters analogous to ones described in the [FaceSDK Parameters](#facesdk-parameters) section. Their default values are (default, true, true).

- **HandleArbitraryRotations, DetermineFaceRotationAngle, InternalResizeWidth** - the parameters analogous to ones in [FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function). Their default values are (false, false, 256).

- **FaceDetectionThreshold** - a parameter analogous to one in [FSDK_SetFaceDetectionThreshold](#fsdk_setfacedetectionthreshold-function). The default value is 5.

- **FaceTrackingDistance** - specifies the maximum distance between faces of one person on consecutive frames, to consider an uninterrupted tracking sequence. The parameter is measured in width of the detected face. The default value is 0.5. You may decrease it when the frame rate is high to lower the probability of false acceptances, or increase it when the frame rate is low and the recognition rate is low due to interrupted tracking.

<a id="face-recognition-parameters"></a>
### Face recognition parameters

- **RecognizeFaces** - whether to recognize subject's identity. If set to true, the system attempts to assign each subject a unique id, while giving equal identifiers to the same subject across the video. If set to false, the system will return a unique ID value for every uninterrupted sequence of a detected face (that is, when a certain face is detected on every frame of the sequence), regardless of the identity of this face. The default value is true.

- **DetectGender** - whether to recognize the gender of a subject. Gender recognition requires the detection of facial features, so when set to true, facial features are detected regardless of the DetectFacialFeatures parameter. The default value is false.

- **DetectAge** - whether to recognize the age of a subject. Age recognition requires the detection of facial features, so when set to true, facial features are detected regardless of the DetectFacialFeatures parameter. The default value is false.

- **DetectExpression** - whether to recognize facial expression of a subject. Expression recognition requires the detection of facial features, so when set to true, facial features are detected regardless of the DetectFacialFeatures parameter. The default value is false.

- **DetectLiveness** - whether to perform passive liveness detection. See the [Passive Liveness](#passive-liveness) section for more details. The default value is false.

- **Learning** - whether to learn subjects' appearances. If set to true, the API will learn the appearance of each subject, unless its memory is full, and add new subjects to the memory. If set to false, the system will return only the identifiers already present in the memory; no addition of novel subjects, novel facial appearances, or merger of identifiers will occur. If a subject does not match any appearance stored in the memory, [FSDK_FeedFrame](#fsdk_feedframe-function) will return the -1 identifier for that subject. Set this flag to false if you have a reason not to alter the memory. The default value is true.

- **MemoryLimit** - the amount of memory available for the storage of facial appearances. See the [Tracker Memory](#tracker-memory) section. The default value is 2150.

- **Threshold** - the threshold used when deciding if two facial appearances belong to the same subject. Each threshold value alters both the false acceptance rate and recognition rate. See the [Recognition Performance](#recognition-performance) section. The default value is 0.992.

- **KeepFaceImages** - whether to store the original facial images in the Tracker memory. See the [Storing original facial images](#storing-original-facial-images) section for details. The default value is true.

<a id="facial-feature-tracking-parameters"></a>
### Facial feature tracking parameters

- **DetectEyes** - whether to detect eyes. Eyes will be detected regardless of the value of this parameter when *RecognizeFaces* is set to 1. When eyes are detected, their coordinates can be retrieved with [FSDK_GetTrackerEyes](#fsdk_gettrackereyes-function). The default value is false.

- **DetectFacialFeatures** - whether to detect facial features. Facial features are detected when *RecognizeFaces* is set to 1, regardless of the value of this parameter. They are also detected if DetectGender, DetectAge or DetectExpression are set to 1. The default value is false.

- **DetectAngles** - whether to estimate out-of-plane face rotation angles by using the detected facial features. Pan and Tilt are returned as the Angles facial attribute. The default value is false.

- **FacialFeatureJitterSuppression** - whether to suppress the jitter of facial features by employing more processor resources. If 0, such jitter suppression is not employed. Set to a higher value for better suppression. A non-zero setting takes effect only when DetectFacialFeatures=true, even if facial features are actually detected due to the setting of the RecognitionPrecision, DetectGender, DetectAge or DetectExpression parameters. The default value depends on NUM_THREADS, the number of threads supported by the CPU, which can be obtained using the [FSDK_GetNumThreads](#fsdk_getnumthreads-function) function.

- **SmoothFacialFeatures** - whether to smooth facial features from frame to frame to prevent jitter. If set to false, the coordinates of facial features are detected independently of the previous frame, and may jitter because of the noise present in the video. If the parameter is set to true, the API will smooth the coordinates of facial features. The default value is true.

- **FacialFeatureSmoothingSpatial** - a coefficient employed in facial feature smoothing. Controls spatial smoothing of facial features. The default value is 0.5.

- **FacialFeatureSmoothingTemporal** - a coefficient employed in facial feature smoothing. Affects temporal smoothing of facial features (that is, how the smoothed coordinates relate to their coordinates on the previous frame). The default value is 250.

---

<a id="tuning-for-optimal-performance"></a>
## Tuning for Optimal Performance

The higher the frame rate of [FSDK_FeedFrame](#fsdk_feedframe-function) (i.e., fast processing of frames) usually positively affect the recognition rate for live video, because more facial appearances of a person can be captured per unit of time.

Experiment with face detection parameters, especially with InternalResizeWidth: higher values allow for faces to be detected at greater distance, but require additional time (and lower the frame rate). If you find a high number of false detections (i.e. when faces are detected where they are not present), try increasing the FaceDetectionThreshold parameter.

Setting DetectGender, DetectAge or DetectExpression to true will lower the frame rate. If you need only to detect gender, age or facial expressions, you may consider setting the RecognizeFaces parameter to false, in order to increase the frame rate.

---

<a id="complete-tracker-api-setup-example"></a>
## Complete Tracker API Setup Example

Below are complete, working examples showing how to set up the Tracker API for continuous face tracking in a live video stream, including initialization, configuration, the frame processing loop, and proper cleanup. Note that this is a minimal demo that processes about 1000 frames and exits cleanly. In a real application, you would typically run the frame processing loop indefinitely in a separate thread until the user decides to exit.

<a id="c-example"></a>
### C++ Example

```cpp
#include "LuxandFaceSDK.h"
#include <cstdio>
#include <cstring>
#include <thread>
#include <chrono>

int main() {
    // Step 1: Initialize and activate FaceSDK
    if (FSDK_Initialize("") != FSDKE_OK) {
        printf("Failed to initialize FaceSDK\n");
        return 1;
    }
    FSDK_ActivateLibrary("your-license-key");

    // Step 2: Initialize video capturing subsystem
    if (FSDK_InitializeCapturing() != FSDKE_OK) {
        printf("Failed to initialize capturing\n");
        return 1;
    }

    // Step 3: Create a tracker
    HTracker tracker;
    if (FSDK_CreateTracker(&tracker) != FSDKE_OK) {
        printf("Failed to create tracker\n");
        return 1;
    }

    // Step 4: Configure tracker parameters
    int errpos;
    FSDK_SetTrackerMultipleParameters(tracker,
        "RecognizeFaces=true;"
        "DetectGender=true;"
        "DetectAge=true;"
        "DetectExpression=true;"
        "Threshold=0.992",
        &errpos);

    // Step 5: Get camera list and open the first available camera
    char** cameraNames;
    int cameraCount;
    if (FSDK_GetCameraList(&cameraNames, &cameraCount) != FSDKE_OK || cameraCount == 0) {
        printf("No cameras found\n");
        FSDK_FreeTracker(tracker);
        return 1;
    }

    // Optionally, set the video format for the selected camera
    int formatCount;
    FSDK_VideoFormatInfo* formatList;
    FSDK_GetVideoFormatList(cameraNames[0], &formatList, &formatCount);
    if (formatCount > 0) {
        FSDK_SetVideoFormat(cameraNames[0], formatList[0]);
        FSDK_FreeVideoFormatList(formatList);
    }

    int cameraHandle;
    if (FSDK_OpenVideoCamera(cameraNames[0], &cameraHandle) != FSDKE_OK) {
        printf("Failed to open camera: %s\n", cameraNames[0]);
        FSDK_FreeCameraList(cameraNames, cameraCount);
        FSDK_FreeTracker(tracker);
        return 1;
    }
    FSDK_FreeCameraList(cameraNames, cameraCount);

    // Step 6: Frame processing loop
    HImage frame;
    long long IDs[256];
    long long faceCount;
    const int maxFrames = 1000;  // Minimal demo: process ~1000 frames and exit cleanly
    int processedFrames = 0;

    while (processedFrames < maxFrames) {
        if (FSDK_GrabFrame(cameraHandle, &frame) != FSDKE_OK) {
            std::this_thread::sleep_for(std::chrono::milliseconds(10));
            continue;
        }

        // Feed frame to tracker — returns IDs of detected faces
        FSDK_FeedFrame(tracker, cameraHandle, frame, &faceCount, IDs, sizeof(IDs));

        for (int i = 0; i < faceCount; i++) {
            // Get face position
            TFacePosition facePos;
            FSDK_GetTrackerFacePosition(tracker, cameraHandle, IDs[i], &facePos);

            // Get name (if tagged)
            char name[256];
            FSDK_GetAllNames(tracker, IDs[i], name, sizeof(name));

            // Get attributes
            char attrs[1024];
            FSDK_GetTrackerFacialAttribute(tracker, cameraHandle, IDs[i],
                "Gender;Age;Expression", attrs, sizeof(attrs));

            printf("ID %lld at (%d,%d) size=%d: %s %s\n",
                IDs[i], facePos.xc, facePos.yc, facePos.w,
                strlen(name) > 0 ? name : "Unknown", attrs);
        }

        FSDK_FreeImage(frame);
        processedFrames++;
    }

    // Step 7: Cleanup (in reverse order of creation)
    FSDK_SaveTrackerMemoryToFile(tracker, "tracker_data.db");
    FSDK_CloseVideoCamera(cameraHandle);
    FSDK_FreeTracker(tracker);
    return 0;
}
```

<a id="python-example"></a>
### Python Example

```python
from fsdk import FSDK
import time

# Initialize
FSDK.Initialize()
FSDK.ActivateLibrary("your-license-key")
FSDK.InitializeCapturing()

# Create and configure tracker
tracker = FSDK.Tracker()
tracker.SetParameters(
    RecognizeFaces=True,
    DetectGender=True,
    DetectAge=True,
    DetectExpression=True,
    Threshold=0.992
)

# Get camera list and open the first available camera
camera_names = FSDK.GetCameraList()
if not camera_names:
    raise RuntimeError("No cameras found")

formats = FSDK.GetVideoFormatList(camera_names[0])
if formats:
    FSDK.SetVideoFormat(camera_names[0], formats[0])

camera = FSDK.OpenVideoCamera(camera_names[0])

# Frame processing loop
max_frames = 1000  # Minimal demo: process ~1000 frames and exit cleanly
processed_frames = 0

try:
    while processed_frames < max_frames:
        frame = FSDK.GrabFrame(camera)
        if frame is None:
            time.sleep(0.01)
            continue

        ids = tracker.FeedFrame(frame)

        for face_id in ids:
            position = tracker.GetFacePosition(face_id)
            names = tracker.GetAllNames(face_id)
            attrs = tracker.GetFacialAttribute(face_id, "Gender;Age;Expression")
            print(f"ID {face_id}: {names or 'Unknown'} at {position} — {attrs}")

        FSDK.FreeImage(frame)
        processed_frames += 1
except KeyboardInterrupt:
    pass

# Cleanup
tracker.SaveMemoryToFile("tracker_data.db")
FSDK.CloseVideoCamera(camera)
FSDK.FreeTracker(tracker)
```

<a id="key-setup-considerations"></a>
### Key Setup Considerations

- **Always call FSDK_InitializeCapturing** before opening cameras — this initializes the video capture subsystem.
- **Use [FSDK_GetCameraList](#fsdk_getcameralist-function)** to enumerate available cameras and pass the camera name to [FSDK_OpenVideoCamera](#fsdk_openvideocamera-function). You can optionally query and set the video format with [FSDK_GetVideoFormatList](#fsdk_getvideoformatlist-function) and [FSDK_SetVideoFormat](#fsdk_setvideoformat-function) before opening the camera. Use [FSDK_OpenIPVideoCamera](#fsdk_openipvideocamera-function) for IP/network cameras.
- **Free camera and format lists** after use with [FSDK_FreeCameraList](#fsdk_freecameralist-function) and [FSDK_FreeVideoFormatList](#fsdk_freevideoformatlist-function) to avoid memory leaks.
- **Free each frame** with [FSDK_FreeImage](#fsdk_freeimage-function) after processing to prevent memory accumulation.
- **The second parameter of FSDK_FeedFrame** is the camera handle returned by FSDK_OpenVideoCamera. Use different values when feeding frames from different cameras to the same tracker.
- **Handle FSDK_GrabFrame failures** gracefully — the camera may temporarily fail to deliver a frame (e.g., USB camera disconnect). Skip the frame and retry.

---

<a id="using-the-api"></a>
## Using the API

The API allows for creating several trackers within the program, each having a separate memory for the recognized subjects and their names.

The tracker is represented with the HTracker data type.

**C++ Declaration:**

```cpp
typedef unsigned int HTracker;
```

**Python Declaration:**

```python
class FSDK.Tracker
```

<a id="locking-identifiers"></a>
### Locking identifiers

There are cases when you need to work with (or tag) an identifier across several frames. For example, you may have the user interface running in a different thread than [FSDK_FeedFrame](#fsdk_feedframe-function). Then, there is a chance that when a user selects an untagged identifier and starts to enter a name for it, the identifier may become purged by [FSDK_FeedFrame](#fsdk_feedframe-function) running in parallel (see the Tracker Memory section). To prevent this, you need to use the [FSDK_LockID](#fsdk_lockid-function) function as soon as the user selected an identifier. The function will prevent the untagged identifier from being purged completely.

<a id="multiple-camera-support"></a>
### Multiple camera support

Tracker API is designed to support multiple cameras, though in the current release only a single camera is supported. You should pass 0 as the CameraIdx parameter to every function that accepts it. You should not alternate frames from multiple cameras while sending them to [FSDK_FeedFrame](#fsdk_feedframe-function), since it will disrupt the tracking process, and yield a lower recognition rate and a higher false acceptance rate. It is also not recommended to switch from one camera to another while sending the frames using [FSDK_FeedFrame](#fsdk_feedframe-function). It is acceptable, however, to switch cameras before the memory of the tracker is loaded with [FSDK_LoadTrackerMemoryFromFile](#fsdk_loadtrackermemoryfromfile-function) or [FSDK_LoadTrackerMemoryFromBuffer](#fsdk_loadtrackermemoryfrombuffer-function).

<a id="storing-original-facial-images"></a>
### Storing original facial images

As the internal format of facial appearances may change in future versions of FaceSDK, Tracker API has the KeepFaceImages parameter, which controls whether the original facial images are stored in the Tracker memory. If the format changes, you will be able to convert your Tracker memory to the new format automatically (if you've stored the original facial images). In such a case, you won't need to reenroll your subjects. It is recommended that you keep this parameter set to true, its default setting.

When the KeepFaceImages parameter is set to true, Tracker API stores an original facial image along with every facial appearance in the Tracker memory. The size of a facial appearance is about 1.5 Kbytes when KeepFaceImages is set to false, and about 11 Kbytes when KeepFaceImages is set to true. Note that if you've had this parameter set to false and accumulated some facial appearances, their original facial images will be lost, even if you set KeepFaceImages to true after that.

If you don't want the original facial images to be stored in the Tracker memory, set this parameter to false.

---

<a id="usage-scenario"></a>
## Usage Scenario

The following scenario is employed when using Tracker API.

1. Create a tracker ([FSDK_CreateTracker](#fsdk_createtracker-function)) or load it from a file ([FSDK_LoadTrackerMemoryFromFile](#fsdk_loadtrackermemoryfromfile-function)) or from a memory buffer ([FSDK_LoadTrackerMemoryFromBuffer](#fsdk_loadtrackermemoryfrombuffer-function)).

2. Set tracker parameters ([FSDK_SetTrackerParameter](#fsdk_settrackerparameter-function), [FSDK_SetTrackerMultipleParameters](#fsdk_settrackermultipleparameters-function)), such as face detection parameters, recognition precision, or the option to recognize gender/age/facial expression or to detect facial features.

3. Open a video camera ([FSDK_OpenVideoCamera](#fsdk_openvideocamera-function), [FSDK_OpenIPVideoCamera](#fsdk_openipvideocamera-function)), or prepare to receive video frames from another source.

4. In a loop:
   1. Receive a frame from a camera ([FSDK_GrabFrame](#fsdk_grabframe-function)) or another source.
   2. Send the image to the [FSDK_FeedFrame](#fsdk_feedframe-function) function.
   3. Display the image on a screen.
   4. For each ID returned by [FSDK_FeedFrame](#fsdk_feedframe-function):
      - Retrieve its facial coordinates ([FSDK_GetTrackerFacePosition](#fsdk_gettrackerfaceposition-function)), eye center coordinates ([FSDK_GetTrackerEyes](#fsdk_gettrackereyes-function)), facial feature coordinates ([FSDK_GetTrackerFacialFeatures](#fsdk_gettrackerfacialfeatures-function)), gender, age or facial expression ([FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function)).
      - Retrieve the list of possible names ([FSDK_GetAllNames](#fsdk_getallnames-function)).
      - If, relying on coordinates, you found that user has clicked on a face, call [FSDK_LockID](#fsdk_lockid-function) on that identifier, display an input box and ask the user for a name of the subject. You may continue to run [FSDK_FeedFrame](#fsdk_feedframe-function) in parallel.
      - If the user entered a name, set it using [FSDK_SetName](#fsdk_setname-function). If the user chose to erase the subject, call [FSDK_SetName](#fsdk_setname-function) with an empty name. In any case, call [FSDK_UnlockID](#fsdk_unlockid-function) to unlock the identifier.
      - If manually handling identifiers, call [FSDK_GetSimilarIDCount](#fsdk_getsimilaridcount-function) and [FSDK_GetSimilarIDList](#fsdk_getsimilaridlist-function) to retrieve similar identifiers, and call [FSDK_GetIDReassignment](#fsdk_getidreassignment-function) for every previously stored identifier before comparing against them.
   5. If necessary, save tracker memory to a file or a buffer ([FSDK_SaveTrackerMemoryToFile](#fsdk_savetrackermemorytofile-function), [FSDK_SaveTrackerMemoryToBuffer](#fsdk_savetrackermemorytobuffer-function)).

5. Free the tracker handle using [FSDK_FreeTracker](#fsdk_freetracker-function).

6. Close the video camera ([FSDK_CloseVideoCamera](#fsdk_closevideocamera-function)).

---

<a id="using-tracker-as-database-of-face-templates"></a>
## Using Tracker as database of face templates

The user can manage face tamples stored in the tracker database. For example, the new face templates can be added and removed from the Tracker. The tracker can also find similar face templaes with high speed.

<a id="user-interaction-with-the-system"></a>
## User Interaction with the System

In a typical scenario, a user observes the images from a camera, with faces outlined in rectangles and names displayed under the rectangles. There is an option to tag a subject with a name by clicking its face and entering the name, or to remove the subject from the memory. The software may notify the user when some previously defined subjects appear. The software may additionally store each image of a subject, and allow browsing such subject's images. The software may store images of untagged subjects as well (and store their ID along with the image), but keep in mind that if the memory limit is reached, earlier appearances of untagged subjects will be purged, and should these subjects appear again, they may be given with new ID numbers (unrelated to their old identifiers; see the [Tracker Memory](#tracker-memory) section).

The user normally should have control over the MemoryLimit and Threshold parameters to alter the recognition quality and the number of subjects that can be stored in the system.

<a id="enrollment"></a>
### Enrollment

To enroll a subject, the user is usually only required to click a subject's face and enter the name. If the subject has been already present in front of the camera for a certain time (for example, while approaching the user's desk), it is likely that the API has stored enough facial appearances of the subject to recognize it again. If this is not the case, the subject may be asked to tilt or rotate its head, to walk closer to or further away from the camera, and the lighting can be altered. If the frame rate is especially low, or if environmental conditions change unexpectedly, the API may not recognize the subject in some appearances. In such cases, the user may tag a subject with the same name on several occasions, until enough facial appearances are stored, and the subject is consistently recognized.

If you need to ensure that you track a live subject, consider detecting whether the facial expression changes with the [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function) function.

<a id="dealing-with-false-acceptances"></a>
### Dealing with false acceptances

The API is designed to return several names with [FSDK_GetAllNames](#fsdk_getallnames-function) for a certain ID. In most cases, the system will return only a single name. If the system returns several names, it means that a false acceptance has occurred. That is, two (or more) subjects became confused.

Although the false acceptance rate is usually low, there is no way to eliminate it completely; instead, the user balances the false acceptance rate against the recognition rate. The software should account for the scenario when a false acceptance has occurred.

In an access control setting, you may decide to grant access to the subject if any of the names recognized has the appropriate permissions. Alternatively, the software may signal about a false acceptance, and the user may decide to set the Threshold parameter to a higher value - to lower the probability of next false acceptance. In that case it is necessary, first, to erase the persons that were confused (by calling [FSDK_SetName](#fsdk_setname-function) with an empty name to remove the name, and [FSDK_PurgeID](#fsdk_purgeid-function) to remove all facial appearances of this ID), and then, when the threshold is set to a higher value, to set their names again.

Keep in mind that not every false acceptance will return several names of a person. It is possible that just a single incorrect name is returned, and the false acceptance may go unnoticed. However, with the appropriate setting of the Threshold parameter, such scenarios are rare.

Note that when there are one or more similar identifiers returned with [FSDK_GetSimilarIDList](#fsdk_getsimilaridlist-function), and these identifiers do not have name tags, this does not always mean a false acceptance. As described in the [Understanding Identifiers](#understanding-identifiers) section, when the memory for an identifier is full, it will not become merged with other identifiers (even if they represent the same subject), so these identifiers will be returned in the list of similar identifiers.

---

<a id="saving-and-loading-tracker-memory"></a>
## Saving and Loading Tracker Memory

To save the memory of a tracker to file, use the [FSDK_SaveTrackerMemoryToFile](#fsdk_savetrackermemorytofile-function) function. Alternatively, you may save it to a memory buffer (for example, for later importing into a database). You need to call [FSDK_GetTrackerMemoryBufferSize](#fsdk_gettrackermemorybuffersize-function) to determine the size of the buffer, and then call [FSDK_SaveTrackerMemoryToBuffer](#fsdk_savetrackermemorytobuffer-function).

Conversely, to load the memory of a tracker from a file or a buffer, use the [FSDK_LoadTrackerMemoryFromFile](#fsdk_loadtrackermemoryfromfile-function) or [FSDK_LoadTrackerMemoryFromBuffer](#fsdk_loadtrackermemoryfrombuffer-function) functions. Note that you need to set the tracker parameters again after loading, because a new tracker handle has been created, with parameters set to default values.

Note that this operation saves only the memory contents of a tracker: stored facial appearances, identifiers, and names. The parameters of a tracker are not saved. Moreover, the internal state of face tracking is not saved as well. It means that if, during the main loop (where you call [FSDK_FeedFrame](#fsdk_feedframe-function)), you save the tracker to a file, and then immediately reload it, such an operation will disrupt face tracking. Because of this, the later recognition results you receive will be different (compared to when such an operation was not done), and the parameters will be reset to defaults. Also, you will not be able to receive face position, eye coordinates, facial feature coordinates, or get the list of similar identifiers immediately after loading. However, after the next [FSDK_FeedFrame](#fsdk_feedframe-function) call, face tracking resumes, and the aforementioned functions operate normally.

---

<a id="recognition-performance"></a>
## Recognition Performance

The performance of face recognition (i.e. how often a subject is recognized, and how often different subjects are confused) is controlled with the Threshold and MemoryLimit parameters. The higher the Threshold parameter (and the lower the MemoryLimit parameter), the less often a subject will be recognized, and the less often confusions will occur.

<a id="performance-measures"></a>
### Performance measures

Tracker API employs two performance measures: false acceptance rate (**FAR**) and recognition rate (**R**). **FAR** measures the rate of confusing different subjects (that is, assigning different subjects with equal identifier values) during a certain number of storage events, once the memory becomes full. **R** measures the rate of recognizing a person after tagging, once all available memory is full.

<a id="understanding-storage-events"></a>
### Understanding storage events

When calculating **FAR**, one could just count how often false acceptances occur during a certain time interval (for example, an hour). However, such a measure will vary greatly across different kinds of video footage.

For example, in an office setting, when subjects are sitting at their desks, and change their positions or facial expressions rather slowly, almost every frame will be very similar to the previous one. Therefore, the API will store novel facial appearances at a slow pace. If there were no false acceptances on a previous frame, they are very unlikely to occur on the next; therefore we expect false acceptances to occur rather rarely.

On the other hand, in an active setting (when many novel subjects appear in front of the camera, move around, and disappear from view), we expect the system to store novel facial appearances quite often, because many subjects appear at previously unseen views. Therefore, we expect false acceptances to occur more often, because of the faster pace of the video.

To employ a rate that is meaningful in both settings, we instead measure time not in seconds, but in storage events. For example, in the office setting, at 12 frames per second, we may get only 400 storage events during an hour, and in the active setting we may get 3600 storage events during an hour. We measure FAR at an interval of 2000 storage events, which could be roughly equal to 5 hours of a hypothetical less active setting, or 32 minutes of an active setting. It is important to note that as facial appearances of a subject accumulate, the rate of storage events will slow down, since there will be fewer novel facial appearances.

<a id="how-to-measure-your-rate-of-storage-events"></a>
### How to measure your rate of storage events

To measure the rate of storage events in your setting, call [FSDK_GetTrackerParameter](#fsdk_gettrackerparameter-function) with the MemorySize parameter during the main loop. Each time a storage event occurs, the MemorySize parameter increases. As your video progresses, you may calculate how much time will be needed to reach 2000 storage events. Note that when the memory is full, storage events themselves still occur, but nothing is stored; this does not mean that FAR becomes zero. You should estimate the rate of storage events before the memory is full.

<a id="understanding-far"></a>
### Understanding FAR

**FAR** is the rate of assigning different subjects with equal identifier values. The rate tells how often a certain subject (say, John) will be falsely accepted as any other subject. For example, if **FAR** is 0.001, John might expect a 0.001 probability of being falsely accepted as some other subject. However, if we have 10 subjects in the system, such a rate applies to every one of them. Therefore, it is practical to know the rate of falsely accepting at least two subjects among any of them. Such a rate can be calculated as:

$$
1 - \left(1 - \mathrm{FAR}\right)^{\frac{N(N-1)}{2}}
$$

where N is the number of subjects. For example, at FAR=0.001, N=10, we have a 4.4% rate that at least one false acceptance will occur during the 2000 storage events considered. To have a 1% rate with 10 subjects, FAR should not exceed 0.0003.

<a id="understanding-r"></a>
### Understanding R

**R** is the rate of recognizing a subject after it was tagged a single time, and all memory available for a subject becomes full. A subject is successfully recognized if its name is present among the names returned by [FSDK_GetAllNames](#fsdk_getallnames-function). R is measured from 0 to 1, which translates to recognition in 0% and 100%, respectively, of frames received by FSDK_FeedFrame.

**R** depends mainly on the amount of memory available for each subject. For example, if there are 30 subjects in your system, and you allow 20 units of memory for each subject, your memory limit should be (30+1)*20=620.

<a id="choosing-threshold-value"></a>
### Choosing Threshold value

To choose the Threshold value, refer to the tables below. You should consider the maximum number of subjects to be tagged within your system, and the maximum memory per subject.

Generally, the higher the MemoryLimit is set, the higher the FAR will be (once all available memory has been used).

Note that higher Threshold values together with a higher memory amount allow higher recognition rate *only* when enough facial appearances of an identifier have been accumulated. If there are sudden changes in facial appearance (due to low frame rate or environmental factors, for example), it may require more time to capture enough facial appearances with a higher Threshold value.

The tables below show the expected false acceptance rate and recognition rate.

**Note:** it is not recommended to use Threshold higher than 0.999, since it will make Tracker API recognize faces less often.

<a id="false-acceptance-rate-at-threshold-and-memorylimit"></a>
### False Acceptance Rate at Threshold and MemoryLimit

| Threshold | 350 | 700 | 1750 | 3500 | 5250 | 7500 |
|---|---|---|---|---|---|---|
| 0.992000 | 0.000081 | 0.000130 | 0.000231 | 0.000266 | 0.000277 | 0.000277 |
| 0.993141 | 0.000066 | 0.000107 | 0.000183 | 0.000209 | 0.000216 | 0.000216 |
| 0.994283 | 0.000062 | 0.000089 | 0.000144 | 0.000166 | 0.000170 | 0.000170 |
| 0.995424 | 0.000052 | 0.000068 | 0.000101 | 0.000114 | 0.000118 | 0.000118 |
| 0.996566 | 0.000042 | 0.000050 | 0.000072 | 0.000077 | 0.000081 | 0.000081 |
| 0.997707 | 0.000036 | 0.000040 | 0.000054 | 0.000055 | 0.000056 | 0.000056 |
| 0.998849 | 0.000030 | 0.000034 | 0.000045 | 0.000039 | 0.000039 | 0.000039 |
| 0.999990 | 0.000002 | 0.000007 | 0.000009 | 0.000012 | 0.000014 | 0.000023 |

<a id="recognition-rate-at-threshold-and-memory-per-subject"></a>
### Recognition Rate at Threshold and Memory per subject

| Threshold | 5 | 10 | 15 | 21 |
|---|---|---|---|---|
| 0.992000 | 0.995 | 0.999 | 0.999 | 0.999 |
| 0.993141 | 0.994 | 0.999 | 0.999 | 0.999 |
| 0.994283 | 0.993 | 0.998 | 0.999 | 0.999 |
| 0.995424 | 0.991 | 0.998 | 0.998 | 0.998 |
| 0.996566 | 0.986 | 0.997 | 0.997 | 0.997 |
| 0.997707 | 0.978 | 0.995 | 0.996 | 0.996 |
| 0.998849 | 0.956 | 0.986 | 0.988 | 0.988 |
| 0.999990 | 0.073 | 0.087 | 0.107 | 0.138 |

For example, let us assume that you have 30 subjects in an office setting, your frame rate is 12 per second, and you decide to allow 21 units of memory per subject. Therefore, your memory limit is (30+1)*21 = 651 (see formula in the [Memory available for each subject](#memory-available-for-each-subject) section). You decide to have a FAR of 0.000050 and calculate that with 30 subjects, there will be 2.2% rate that a subject will be given with an ID of any other subject (see the formula in the [Understanding FAR](#understanding-far) section) during 2000 storage events (approximately 5 hours in an office setting). To have a FAR of 0.000050 with MemoryLimit=700 (the value closest to 651 in the table), you choose Threshold=0.996566. You note that at such a threshold and 21 units of memory per subject, you have a 0.997 recognition rate (meaning subjects will be recognized in 99.7% of frames in the video).

---

<a id="gender-age-and-facial-expression-recognition"></a>
## Gender, Age and Facial Expression Recognition

The API allows for identifying gender and age of a face and its expressions by using the [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function) function.

To detect gender, you need to set the DetectGender tracking parameter to true. The function returns confidence levels for each gender (male and female) in the output string. You can parse this string using the [FSDK_GetValueConfidence](#fsdk_getvalueconfidence-function) function.

To detect age, you need to set the DetectAge tracking parameter to true. The function then returns the age of the face in the output string.

To detect expression, you need to set the DetectExpression tracking parameter to true. The function returns confidence levels for each expression (if a smile is present and if the eyes are open or closed) in the output string. You can parse this string using the [FSDK_GetValueConfidence](#fsdk_getvalueconfidence-function) function.

The confidence level for each attribute, returned by the [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function) function, varies from 0 to 1 (except the "Age" attribute - for which the age itself - not a confidence level, is returned). When recognizing gender, you may assume that the recognized gender will be the one with the higher confidence level.

If your system should respond to the particular gender of a novel subject (for example, when advertising separate products for male and female visitors), consider waiting for about a second after the subject has first appeared, for the gender to be recognized with higher accuracy. You may also consider responding when the confidence level is not just merely greater than 0.5, but exceeds a certain threshold (for example, 0.7 or 0.9, which translate to 70% or 90% accuracy).

If your system should respond to the particular expression of a subject (for example, taking a picture only when a person smiles and the eyes are open), consider waiting for about 0.5 seconds after the subject has appeared. To find out if the expression is present, it is usually optimal to compare the confidence in the attribute value with the 0.5 threshold (i.e., if the confidence in the "Smile" value is greater than 0.5, the person smiles, and if the confidence in the "EyesOpen" value is greater than 0.5, the eyes are open). You may use a higher threshold for greater certainty, but in this case some expressions may not be detected.

Note that gender, age and expression recognition requires the detection of facial features, so facial features will be detected regardless of the DetectFacialFeatures parameter value. This will decrease the frame rate. You might consider setting the RecognizeFaces parameter to false if you only need to detect gender, age or expressions and do not need recognition of the subjects' identities, which will increase the frame rate.

---

<a id="face-eye-and-facial-feature-tracking"></a>
## Face, Eye and Facial Feature Tracking

Tracker API supports the tracking of face, eye centers, and facial features in addition to the recognition of a subject's identity. You need to use the [FSDK_GetTrackerFacePosition](#fsdk_gettrackerfaceposition-function), [FSDK_GetTrackerEyes](#fsdk_gettrackereyes-function) and [FSDK_GetTrackerFacialFeatures](#fsdk_gettrackerfacialfeatures-function) to retrieve the corresponding coordinates. You also need to set the parameter DetectEyes or DetectFacialFeatures to true when tracking eyes or facial features, respectively. Tracker API performs smoothing of facial features (see the SmoothFacialFeatures parameter).

When you only need to track faces, and do not need to recognize subjects' identities, you can disable face recognition to improve performance. To accomplish that, you need to set the RecognizeFaces parameter to false.

<a id="counting-the-number-of-people"></a>
### Counting the number of people

You should not estimate the amount of people the system observed based on the values of the identifiers, since some of they may have been merged with others. Instead, you may retain all the ID values returned by Tracker API, and at the point when the number of people should be estimated, you should replace each ID with the value returned by the [FSDK_GetIDReassignment](#fsdk_getidreassignment-function) function. Then, you can count the amount of different identifiers in the list. Note that if memory limit is approached, some untagged identifiers may be purged, and the amount of people may be overestimated. See the [User Interaction with the System](#user-interaction-with-the-system) section for details.

If each subject captured by the camera appears only once, you may consider not determining the subject's identity (set RecognizeFaces to false). Then, the value of the ID returned by the API will be equal to the total number of continuous facial sequences, or approximately the number of people appeared in front of the camera.

---

<a id="thread-safety"></a>
## Thread Safety

All tracker functions are thread safe. Note that you should avoid calling [FSDK_FeedFrame](#fsdk_feedframe-function) simultaneously on the same tracker and camera (the CameraIdx parameter) from several threads, since it will disrupt the [FSDK_GetTrackerEyes](#fsdk_gettrackereyes-function), [FSDK_GetTrackerFacialFeatures](#fsdk_gettrackerfacialfeatures-function), [FSDK_GetTrackerFacePosition](#fsdk_gettrackerfaceposition-function), [FSDK_GetTrackerFacialAttribute](#fsdk_gettrackerfacialattribute-function), [FSDK_GetSimilarIDCount](#fsdk_getsimilaridcount-function), [FSDK_GetSimilarIDList](#fsdk_getsimilaridlist-function) and [FSDK_GetAllNames](#fsdk_getallnames-function) functions. The reason is that the ID received from [FSDK_FeedFrame](#fsdk_feedframe-function) must be passed to these functions before the next [FSDK_FeedFrame](#fsdk_feedframe-function) is executed with the following frame; otherwise these functions may not perform correctly.

<a id="tracker-functions"></a>
# Tracker Functions

<a id="fsdk_createtracker-function"></a>
## FSDK_CreateTracker Function

Creates a new tracker handle to be passed to other Tracker API functions.

**C++ Syntax:**

```cpp
int FSDK_CreateTracker(HTracker * Tracker);
```

**Delphi Syntax:**

```pascal
function FSDK_CreateTracker(Tracker: PHTracker): integer;
```

**C# Syntax:**

```csharp
int FSDK.CreateTracker(ref int Tracker);
```

**Java and Android Syntax:**

```java
int FSDK.CreateTracker(HTracker Tracker);
```

**Parameters:**

- **Tracker** - pointer to the integer variable that will to store the created tracker handle.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.CreateTracker() -> Tracker;

# constructor
Tracker() -> Tracker
```

**Return Value:**

New Tracker object.

---

<a id="fsdk_freetracker-function"></a>
## FSDK_FreeTracker Function

Frees a tracker handle. The handle becomes invalid, and all memory associated with it is released. You should not pass the tracker handle to any other Tracker API functions after the handle was freed.

**C++ Syntax:**

```cpp
int FSDK_FreeTracker(HTracker Tracker);
```

**Delphi Syntax:**

```pascal
function FSDK_FreeTracker(Tracker: HTracker): integer;
```

**C# Syntax:**

```csharp
int FSDK.FreeTracker(int Tracker);
```

**Java and Android Syntax:**

```java
int FSDK.FreeTracker(HTracker Tracker);
```

**Parameters:**

- **Tracker** - handle of the tracker to be freed.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.FreeTracker(tracker: Tracker);

def Tracker.Free();
```

**Note:**

Tracker object is freed automatically by destructor.

---

<a id="fsdk_cleartracker-function"></a>
## FSDK_ClearTracker Function

Clears the content of a tracker, releasing all its memory. The tracker handle stays valid. The parameters are reset to their default values, so if you just need to clear the tracker's memory, consider setting the parameters with the FSDK_SetTrackerParameter or the FSDK_SetTrackerMultipleParameters function again.

**C++ Syntax:**

```cpp
int FSDK_ClearTracker(HTracker Tracker);
```

**Delphi Syntax:**

```pascal
function FSDK_ClearTracker(Tracker: HTracker): integer;
```

**C# Syntax:**

```csharp
int FSDK.ClearTracker(int Tracker);
```

**Java and Android Syntax:**

```java
int FSDK.ClearTracker(HTracker Tracker);
```

**Parameters:**

- **Tracker** - handle of the tracker to be cleared.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.ClearTracker(tracker: Tracker);

def Tracker.Clear();
```

---

<a id="fsdk_settrackerparameter-function"></a>
## FSDK_SetTrackerParameter Function

Sets the parameter of a tracker. See the Tracker Parameters section for details.

**C++ Syntax:**

```cpp
int FSDK_SetTrackerParameter(HTracker Tracker, const char * ParameterName, const char * ParameterValue);
```

**Delphi Syntax:**

```pascal
function FSDK_SetTrackerParameter(Tracker: HTracker; ParameterName, ParameterValue: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetTrackerParameter(int Tracker, string ParameterName, string ParameterValue);
```

**Java and Android Syntax:**

```java
int FSDK.SetTrackerParameter(HTracker Tracker, String ParameterName, String ParameterValue);
```

**Parameters:**

- **Tracker** - handle of the tracker to have parameters set parameters.
- **ParameterName** - name of the parameter to be set.
- **ParameterValue** - value of the parameter.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetTrackerParameter(tracker: Tracker, paramName: str, paramValue);

def Tracker.SetParameter(paramName: str, paramValue);
```

**Note:**

The type of *parameterValue* can be of types: str, int, float or bool.

---

<a id="fsdk_settrackermultipleparameters-function"></a>
## FSDK_SetTrackerMultipleParameters Function

Sets multiple parameters of a tracker. The parameters and their values are specified in the following format:

`"Parameter1=Value1[;Parameter2=Value2[;...]]"`

See the Tracker Parameters section for details.

**C++ Syntax:**

```cpp
int FSDK_SetTrackerMultipleParameters(HTracker Tracker, const char * Parameters, int * ErrorPosition);
```

**Delphi Syntax:**

```pascal
function FSDK_SetTrackerMultipleParameters(Tracker: HTracker; Parameters: PAnsiChar; ErrorPosition: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetTrackerMultipleParameters(int Tracker, string Parameters, ref int ErrorPosition);
```

**Java and Android Syntax:**

```java
int FSDK.SetTrackerMultipleParameters(HTracker Tracker, String Parameters, IntByReference ErrorPosition);
```

**Parameters:**

- **Tracker** - handle of the tracker to have parameters set.
- **Parameters** - string containing the parameters and corresponding values to be set.
- **ErrorPosition** - pointer to the integer variable that will receive the position of the character that caused syntax error in the string.

**Return Value:**

Returns FSDKE_OK if successful. In case of syntax error returns FSDKE_SYNTAX_ERROR and sets the value of the ErrorPosition variable.

**Example:**

```cpp
int err = 0;
FSDK_SetTrackerMultipleParameters(tracker, "HandleArbitraryRotations=false; DetermineFaceRotationAngle=false; InternalResizeWidth=100; FaceDetectionThreshold=5;", &err);
```

**Python Syntax:**

```python
def FSDK.SetTrackerMultipleParameters(tracker: Tracker, parameters: str);

def Tracker.SetParameters(**kw);
```

**Note:**

Keyword arguments are interpreted as parameter names with their values to be set.

---

<a id="fsdk_gettrackerparameter-function"></a>
## FSDK_GetTrackerParameter Function

Retrieves the value of a tracker parameter. See the Tracker Parameters section for details.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerParameter(HTracker Tracker, const char * ParameterName, char * ParameterValue, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerParameter(Tracker: HTracker; ParameterName, ParameterValue: PAnsiChar; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerParameter(int Tracker, string ParameterName, out string ParameterValue, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerParameter(HTracker Tracker, String ParameterName, String ParameterValue[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker whose parameter value is desired.
- **ParameterName** - name of the parameter to be retrieved.
- **ParameterValue** - pointer to the output null-terminated string that will store the value of the parameter.
- **MaxSizeInBytes** - amount of memory allocated for the output string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetTrackerParameter(tracker: Tracker, parameterName: str) -> str;

def Tracker.GetParameters(parameterName: str) -> str;
```

**Return Value:**

The value of parameter as string.

---

<a id="fsdk_feedframe-function"></a>
## FSDK_FeedFrame Function

Processes a video frame according to tracker's parameters, and returns the identifiers of the tracked faces. See the Understanding Identifiers, Tracker Memory and Tracker Parameters sections for details.

**C++ Syntax:**

```cpp
int FSDK_FeedFrame(HTracker Tracker, long long CameraIdx, HImage Image, long long * FaceCount, long long * IDs, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_FeedFrame(Tracker: HTracker; CameraIdx: int64; Image: HImage; FaceCount: PInt64; IDs: PIDArray; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.FeedFrame(int Tracker, long CameraIdx, int Image, ref long FaceCount, out long[] IDs, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.FeedFrame(HTracker Tracker, long CameraIdx, HImage Image, long FaceCount[], long IDs[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to process the frame.
- **CameraIdx** - index of the camera; should be equal to 0 in the current release.
- **Image** - the HImage handle of the video frame to process.
- **FaceCount** - address of the 64-bit integer value that will receive the count of faces tracked in the current frame.
- **IDs** - address of the array of 64-bit integer values that will receive the identifiers of the tracked faces.
- **MaxSizeInBytes** - amount of memory allocated for the IDs array.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.FeedFrame(tracker: Tracker, cameraIdx: int, image: Image, maxIDs: int = 512) -> List[int];

def Tracker.FeedFrame(cameraIdx: int, img: Image, maxIDs: int = 512) -> List[int];
```

**Return Value:**

The list of identifiers of the tracked faces.

**Parameters:**

- **maxIDs** - the maximum number of faces tracked in the current frame.

---

<a id="fsdk_gettrackereyes-function"></a>
## FSDK_GetTrackerEyes Function

Retrieves the coordinates of the eye centers of a tracked face. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetTrackerEyes before the next call of FSDK_FeedFrame using the same tracker.

For the function to return the eye center coordinates, at least one of the parameters DetectEyes, DetectFacialFeatures, RecognizeFaces, DetectGender, DetectAge or DetectExpression must be set to true.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerEyes(HTracker Tracker, long long CameraIdx, long long ID, FSDK_Features * FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerEyes(Tracker: HTracker; CameraIdx, ID: int64; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerEyes(int Tracker, long CameraIdx, long ID, out TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.GetTrackerEyes(HTracker Tracker, long CameraIdx, long ID, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.GetTrackerEyes(HTracker Tracker, long CameraIdx, long ID, FSDK_Features FacialFeatures);
```

**Parameters:**

- **Tracker** - handle of the tracker where the coordinates of the eye centers will be retrieved.
- **CameraIdx** - index of the camera; should be equal to 0 in the current release.
- **ID** - identifier of the subject returned by FSDK_FeedFrame, whose eye center coordinates will be received.
- **FacialFeatures** - pointer to the FSDK_Features variable that will receive the eye center coordinates.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call. Returns FSDKE_ATTRIBUTE_NOT_DETECTED if eye centers were not tracked on the previous FSDK_FeedFrame call.

**Python Syntax:**

```python
def FSDK.GetTrackerEyes(tracker: Tracker, cameraIdx: int, ID: int) -> Eyes;

def Tracker.GetEyes(cameraIdx: int, ID: int) -> Eyes;
```

**Return Value:**

The Eyes object.

---

<a id="fsdk_gettrackerfacialfeatures-function"></a>
## FSDK_GetTrackerFacialFeatures Function

Retrieves the coordinates of a tracked face's features. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetTrackerFacialFeatures before the next call of FSDK_FeedFrame with the same tracker.

For the function to return the facial feature coordinates, either of the parameters DetectFacialFeatures, DetectGender, DetectAge or DetectExpression should be set to true. See the Tracker Parameters section for details.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFacialFeatures(HTracker Tracker, long long CameraIdx, long long ID, FSDK_Features * FacialFeatures);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFacialFeatures(Tracker: HTracker; CameraIdx, ID: int64; FacialFeatures: PFSDK_Features): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFacialFeatures(int Tracker, long CameraIdx, long ID, out TPoint[] FacialFeatures);
```

**Java Syntax:**

```java
int FSDK.GetTrackerFacialFeatures(HTracker Tracker, long CameraIdx, long ID, FSDK_Features.ByReference FacialFeatures);
```

**Android Syntax:**

```java
int FSDK.GetTrackerFacialFeatures(HTracker Tracker, long CameraIdx, long ID, FSDK_Features FacialFeatures);
```

**Parameters:**

- **Tracker** - handle of the tracker from which to retrieve the facial feature coordinates.
- **CameraIdx** - index of the camera; should be equal to 0 in the current release.
- **ID** - identifier of the subject returned by FSDK_FeedFrame, whose facial feature coordinates will be received.
- **FacialFeatures** - pointer to the FSDK_Features variable to receive facial feature coordinates.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call. Returns FSDKE_ATTRIBUTE_NOT_DETECTED if facial features were not tracked on the previous FSDK_FeedFrame call.

**Python Syntax:**

```python
def FSDK.GetTrackerFacialFeatures(tracker: Tracker, cameraIdx: int, ID: int) -> Features;

def Tracker.GetFacialFeatures(cameraIdx: int, ID: int) -> Features;
```

**Return Value:**

The Features object.

**Exceptions:**

- FSDK.IdNotFound
- FSDK.AttributeNotDetected

---

<a id="fsdk_gettrackerfaceposition-function"></a>
## FSDK_GetTrackerFacePosition Function

Retrieves the position of a tracked face. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetTrackerFacePosition before the next call of FSDK_FeedFrame with the same tracker.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFacePosition(HTracker Tracker, long long CameraIdx, long long ID, TFacePosition * FacePosition);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFacePosition(Tracker: HTracker; CameraIdx, ID: int64; FacePosition: PFacePosition): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFacePosition(int Tracker, long CameraIdx, long ID, ref TFacePosition FacePosition);
```

**Java Syntax:**

```java
int FSDK.GetTrackerFacePosition(HTracker Tracker, long CameraIdx, long ID, TFacePosition.ByReference FacePosition);
```

**Android Syntax:**

```java
int FSDK.GetTrackerFacePosition(HTracker Tracker, long CameraIdx, long ID, TFacePosition FacePosition);
```

**Parameters:**

- **Tracker** - handle of the tracker from which to retrieve the face position.
- **CameraIdx** - index of the camera; should be equal to 0 in the current release.
- **ID** - identifier of the subject returned by FSDK_FeedFrame whose face position will be received.
- **FacePosition** - pointer to the TFacePosition variable that will receive the face position.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call.

**Python Syntax:**

```python
def FSDK.GetTrackerFacePosition(tracker: Tracker, cameraIdx: int, ID: int) -> FacePosition;

def Tracker.GetFacePosition(cameraIdx: int, ID: int) -> FacePosition;
```

**Return Value:**

The FacePosition object.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_gettrackerfacialattribute-function"></a>
## FSDK_GetTrackerFacialAttribute Function

Given an attribute of a tracked face, retrieves its Values and their Confidences. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetTrackerFacialAttribute before the next call of FSDK_FeedFrame with the same tracker.

The function allows for detecting gender when provided with the "Gender" attribute name, for detecting age when provided with the "Age" attribute name and for detecting expression when provided with the "Expression" attribute name. Refer to the FSDK_DetectFacialAttributeUsingFeatures function description for details on attributes, their Values and Confidences.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFacialAttribute(HTracker Tracker, long long CameraIdx, long long ID, const char * AttributeName, char * AttributeValues, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFacialAttribute(Tracker: HTracker; CameraIdx, ID: int64; AttributeName, AttributeValues: PAnsiChar; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFacialAttribute(int Tracker, long CameraIdx, long ID, string AttributeName, out string AttributeValues, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerFacialAttribute(HTracker Tracker, long CameraIdx, long ID, String AttributeName, String AttributeValues[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker whose attribute will be retrieved.
- **CameraIdx** - index of the camera; should be equal to 0 in the current release.
- **ID** - identifier of a subject returned by FSDK_FeedFrame whose attribute will be retrieved.
- **AttributeName** - name of the attribute.
- **AttributeValues** - pointer to the null-terminated string that will receive the attribute Values and their Confidences.
- **MaxSizeInBytes** - amount of memory allocated for the output string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call. Returns FSDKE_ATTRIBUTE_NOT_DETECTED if the specified attribute was not detected on the previous FSDK_FeedFrame call. Returns FSDKE_UNKNOWN_ATTRIBUTE if the specified attribute name is not supported. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetTrackerFacialAttribute(tracker: Tracker, cameraIdx: int, ID: int, attributeName: str) -> str;

def Tracker.GetFacialAttribute(cameraIdx: int, ID: int, attributeName: str) -> str;
```

**Return Value:**

The attribute Values and their Confidences as string.

**Exceptions:**

- FSDK.IdNotFound
- FSDK.AttributeNotDetected
- FSDK.UnknownAttribute

---

<a id="fsdk_lockid-function"></a>
## FSDK_LockID Function

Locks an identifier. When an identifier is locked, at least one facial appearance of an identifier will not be deleted during any possible purge. You should call this function before the FSDK_SetName function. The function has no effect on identifiers which were already tagged with a name. The call should be usually paired with FSDK_UnlockID call. When the user does not set a name to a locked identifier, unlocking it allows it to become purged if necessary for memory efficient memory use.

See the Locking identifiers section for details. You may call this function with any identifier regardless of when it was returned as long as it remains present in the tracker memory.

**C++ Syntax:**

```cpp
int FSDK_LockID(HTracker Tracker, long long ID);
```

**Delphi Syntax:**

```pascal
function FSDK_LockID(Tracker: HTracker; ID: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.LockID(int Tracker, long ID);
```

**Java and Android Syntax:**

```java
int FSDK.LockID(HTracker Tracker, long ID);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to lock an identifier.
- **ID** - identifier of the subject to lock.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID is not present in the tracker memory.

**Python Syntax:**

```python
def FSDK.LockID(tracker: Tracker, ID: int);

def Tracker.LockID(ID: int);
```

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_unlockid-function"></a>
## FSDK_UnlockID Function

Unlocks the ID so it may be purged. You should call this function after the FSDK_LockID call. The function has no effect on identifiers which were already tagged with a name.

See the Locking identifiers section for details. You may call this function with any identifier regardless of when it was returned, as long as it is present in the tracker memory.

**C++ Syntax:**

```cpp
int FSDK_UnlockID(HTracker Tracker, long long ID);
```

**Delphi Syntax:**

```pascal
function FSDK_UnlockID(Tracker: HTracker; ID: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.UnlockID(int Tracker, long ID);
```

**Java and Android Syntax:**

```java
int FSDK.UnlockID(HTracker Tracker, long ID);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to unlock an identifier.
- **ID** - identifier of the subject to unlock.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID is not present in the tracker memory.

**Python Syntax:**

```python
def FSDK.UnLockID(tracker: Tracker, ID: int);

def Tracker.UnLockID(ID: int);
```

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_purgeid-function"></a>
## FSDK_PurgeID Function

Removes all facial appearances of the ID from the tracker memory. You must call this function if there was a false acceptance (see the Dealing with false acceptances section) or if you erroneously assigned equal names to different persons.

**C++ Syntax:**

```cpp
int FSDK_PurgeID(HTracker Tracker, long long ID);
```

**Delphi Syntax:**

```pascal
function FSDK_PurgeID(Tracker: HTracker; ID: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.PurgeID(int Tracker, long ID);
```

**Java and Android Syntax:**

```java
int FSDK.PurgeID(HTracker Tracker, long ID);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to purge an identifier.
- **ID** - identifier of the subject to purge.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID is not present in the tracker memory.

**Python Syntax:**

```python
def FSDK.PurgeID(tracker: Tracker, ID: int);

def Tracker.PurgeID(ID: int);
```

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_getname-function"></a>
## FSDK_GetName Function

Returns the name the identifier has been tagged with. You may call this function with any identifier regardless of when it was returned, as long as it is present in the tracker memory.

**C++ Syntax:**

```cpp
int FSDK_GetName(HTracker Tracker, long long ID, char * Name, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetName(Tracker: HTracker; ID: int64; Name: PAnsiChar; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetName(int Tracker, long ID, out string Name, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetName(int Tracker, long ID, String Name[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to retrieve the name.
- **ID** - identifier of a subject to retrieve the name of.
- **Name** - identifier of the subject whose name is to be retrieved.
- **MaxSizeInBytes** - amount of memory allocated for the output string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available. Returns FSDKE_ID_NOT_FOUND if the specified ID is not present in the tracker memory.

**Python Syntax:**

```python
def FSDK.GetName(tracker: Tracker, ID: int) -> str;

def Tracker.GetName(ID: int) -> str;
```

**Return Value:**

Identifier of the subject whose name is to be retrieved.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_setname-function"></a>
## FSDK_SetName Function

Sets the name of an identifier. To erase the name tag, specify an empty name string. When erasing the name tag because of a false acceptance, or because you erroneously assigned equal names to different persons, you must also call the FSDK_PurgeID function (see the Dealing with false acceptances section). The function will unlock the identifier if the name is successfully set.

You may call this function with any identifier regardless of when it was returned, as long as it is present in the tracker memory.

**C++ Syntax:**

```cpp
int FSDK_SetName(HTracker Tracker, long long ID, const char * Name);
```

**Delphi Syntax:**

```pascal
function FSDK_SetName(Tracker: HTracker; ID: int64; Name: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetName(int Tracker, long ID, string Name);
```

**Java Syntax:**

```java
int FSDK.SetName(HTracker Tracker, long ID, String Name);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to set the name.
- **ID** - identifier of the subject whose name is to be set.
- **Name** - pointer to the null-terminated string containing the name of an identifier.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID is not present in the tracker memory.

Returns FSDKE_INSUFFICIENT_TRACKER_MEMORY_LIMIT if there is not enough room to store the identifier's facial appearances in memory. See the Tracker Memory section for details.

**Python Syntax:**

```python
def FSDK.SetName(tracker: Tracker, ID: int, name: str);

def Tracker.SetName(ID: int, name: str);
```

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_getidreassignment-function"></a>
## FSDK_GetIDReassignment Function

When provided with a subject's ID received on earlier frames, returns the new subject's ID if there was a merger. See the Understanding Identifiers section for details. If an identifier was not merged, the function returns the same ID value in the output variable. Note that the function does not return an error if an identifier is not present in the tracker memory; instead; the same ID value is returned in the output variable.

**C++ Syntax:**

```cpp
int FSDK_GetIDReassignment(HTracker Tracker, long long ID, long long * ReassignedID);
```

**Delphi Syntax:**

```pascal
function FSDK_GetIDReassignment(Tracker: HTracker; ID: int64; ReassignedID: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetIDReassignment(int Tracker, long ID, ref long ReassignedID);
```

**Java and Android Syntax:**

```java
int FSDK.GetIDReassignment(HTracker Tracker, long ID, long ReassignedID[]);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to get the reassigned ID value.
- **ID** - identifier of the subject whose reassigned identifier is sought.
- **ReassignedID** - pointer to the 64-bit integer value that will store the reassigned value of an identifier.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetIDReassignment(tracker: Tracker, ID: int) -> int;

def Tracker.GetIDReassignment(ID: int) -> int;
```

**Return Value:**

Identifier of the subject whose reassigned identifier is sought.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_getsimilaridcount-function"></a>
## FSDK_GetSimilarIDCount Function

Returns the number of identifiers that are similar to a given identifier. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetSimilarIDCount before the next call of FSDK_FeedFrame with the same tracker. See the Understanding Identifiers section for details.

**C++ Syntax:**

```cpp
int FSDK_GetSimilarIDCount(HTracker Tracker, long long ID, long long * Count);
```

**Delphi Syntax:**

```pascal
function FSDK_GetSimilarIDCount(Tracker: HTracker; ID: int64; Count: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetSimilarIDCount(int Tracker, long ID, ref long Count);
```

**Java and Android Syntax:**

```java
int FSDK.GetSimilarIDCount(HTracker Tracker, long ID, long Count[]);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to retrieve the number of similar identifiers.
- **ID** - identifier of the subject for which to return the number of similar identifiers.
- **Count** - pointer to the 64-bit integer value that will store the number of similar identifiers.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call.

**Python Syntax:**

```python
def FSDK.GetSimilarIDCount(tracker: Tracker, ID: int) -> int;

def Tracker.GetSimilarIDCount(ID: int) -> int;
```

**Return Value:**

The number of similar identifiers.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_getsimilaridlist-function"></a>
## FSDK_GetSimilarIDList Function

Returns the list of identifiers that are similar to a given identifier. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetSimilarIDList before the next call of FSDK_FeedFrame with the same tracker. See the Understanding Identifiers section for details.

**C++ Syntax:**

```cpp
int FSDK_GetSimilarIDList(HTracker Tracker, long long ID, long long * SimilarIDList, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetSimilarIDList(Tracker: HTracker; ID: int64; SimilarIDList: PIDArray; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetSimilarIDList(int Tracker, long ID, out long[] SimilarIDList, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetSimilarIDList(HTracker Tracker, long ID, long SimilarIDList[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to get the list of similar identifiers.
- **ID** - identifier of the subject for which to return the list of similar identifiers.
- **SimilarIDList** - pointer to the array of 64-bit integer values that will store the list of similar identifiers.
- **MaxSizeInBytes** - amount of memory allocated for the output array.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetSimilarIDList(tracker: Tracker, ID: int) -> List[int];

def Tracker.GetSimilarIDList(ID: int) -> List[int];
```

**Return Value:**

The list of similar identifiers.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_getallnames-function"></a>
## FSDK_GetAllNames Function

Returns the list of names that an identifier can have. The function accepts the identifier returned by FSDK_FeedFrame. This identifier should be passed to FSDK_GetAllNames before the next call of FSDK_FeedFrame with the same tracker. See the Understanding Identifiers and Dealing with false acceptances sections for details.

The function returns all names that belong to a given identifier, and similar identifiers, separated by a semicolon. The output format is:

`"Name1[;Name2[;...]]"`

You should call this function instead of FSDK_GetName whenever possible, and then parse the returned string for all returned names. Alternatively, you may implement the functionality of FSDK_GetAllNames, calling FSDK_GetName on the given identifier, then FSDK_GetSimilarIDCount and FSDK_GetSimilarIDList to get the list of similar identifiers, then finally call FSDK_GetName on that list.

**C++ Syntax:**

```cpp
int FSDK_GetAllNames(HTracker Tracker, long long ID, char * Names, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetAllNames(Tracker: HTracker; ID: int64; Names: PAnsiChar; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetAllNames(int Tracker, long ID, out string Names, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetAllNames(HTracker Tracker, long ID, String Names[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to retrieve the names.
- **ID** - identifier of the subject whose possible names are to be retrieved.
- **Names** - pointer to the null-terminated string that will receive the possible names of an identifier.
- **MaxSizeInBytes** - amount of memory allocated for the output string.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_ID_NOT_FOUND if the specified ID was not returned by the previous FSDK_FeedFrame call. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetAllNames(tracker: Tracker, ID: int) -> List[str];

def Tracker.GetAllNames(ID: int) -> List[str];
```

**Return Value:**

The list of possible names of an identifier.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_savetrackermemorytofile-function"></a>
## FSDK_SaveTrackerMemoryToFile Function

Saves the memory of a tracker to a file. Note that tracker parameters, along with its face tracking state, are not saved. See the Saving and Loading Tracker Memory section for details.

**C++ Syntax:**

```cpp
int FSDK_SaveTrackerMemoryToFile(HTracker Tracker, const char * FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveTrackerMemoryToFile(Tracker: HTracker; FileName: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveTrackerMemoryToFile(int Tracker, string FileName);
```

**Java and Android Syntax:**

```java
int FSDK.SaveTrackerMemoryToFile(HTracker Tracker, String FileName);
```

**Parameters:**

- **Tracker** - handle of the tracker to save.
- **FileName** - pointer to the null-terminated string containing the name of the file to which the tracker memory will be saved.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_IO_ERROR if an I/O error has occurred.

**Python Syntax:**

```python
def FSDK.SaveTrackerMemoryToFile(tracker: Tracker, fileName: str);

def Tracker.SaveToFile(fileName: str);
```

**Exceptions:**

FSDK.IOError

---

<a id="fsdk_loadtrackermemoryfromfile-function"></a>
## FSDK_LoadTrackerMemoryFromFile Function

Loads the memory of a tracker from a file. Note that tracker parameters, along with its face tracking state, are not loaded. See the Saving and Loading Tracker Memory section for details.

**C++ Syntax:**

```cpp
int FSDK_LoadTrackerMemoryFromFile(HTracker * Tracker, const char * FileName);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadTrackerMemoryFromFile(Tracker: PHTracker; FileName: PAnsiChar): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadTrackerMemoryFromFile(ref int Tracker, string FileName);
```

**Java and Android Syntax:**

```java
int FSDK.LoadTrackerMemoryFromFile(HTracker Tracker, String FileName);
```

**Parameters:**

- **Tracker** - pointer that will store the handle of the loaded tracker.
- **FileName** - pointer to the null-terminated string containing the name of a file from which the tracker memory will be to loaded.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_BAD_FILE_FORMAT if the file has unsupported format. Returns FSDKE_UNSUPPORTED_FILE_VERSION if the file was saved with Luxand FaceSDK of an unsupported version. Returns FSDKE_FILE_NOT_FOUND if there was an error opening the file. Returns FSDKE_IO_ERROR if an I/O error has occurred.

**Python Syntax:**

```python
def FSDK.LoadTrackerMemoryFromFile(fileName: str) -> Tracker;

@staticmethod
def Tracker.FromFile(fileName: str) -> Tracker;
```

**Return Value:**

New Tracker object loaded from file.

**Exceptions:**

- FSDK.IOError
- FSDK.BadFileFormat
- FSDK.UnsupportedFileVersion
- FSDK.FileNotFound

---

<a id="fsdk_gettrackermemorybuffersize-function"></a>
## FSDK_GetTrackerMemoryBufferSize Function

Returns the size of a buffer (in bytes) needed to save the memory of a tracker.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerMemoryBufferSize(HTracker Tracker, long long * BufSize);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerMemoryBufferSize(Tracker: HTracker; BufSize: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerMemoryBufferSize(int Tracker, ref long BufSize);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerMemoryBufferSize(HTracker Tracker, long BufSize[]);
```

**Parameters:**

- **Tracker** - handle of the tracker whose buffer size needs calculation.
- **BufSize** - pointer to the 64-bit integer variable that will store the size of a buffer.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetTrackerMemoryBufferSize(tracker: Tracker) -> int;
```

**Return Value:**

The size of a buffer.

---

<a id="fsdk_savetrackermemorytobuffer-function"></a>
## FSDK_SaveTrackerMemoryToBuffer Function

Saves the memory of a tracker to a buffer. Note that tracker parameters, along with its face tracking state, are not saved. See the Saving and Loading Tracker Memory section for details.

**C++ Syntax:**

```cpp
int FSDK_SaveTrackerMemoryToBuffer(HTracker Tracker, unsigned char * Buffer, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_SaveTrackerMemoryToBuffer(Tracker: HTracker; var Buffer; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.SaveTrackerMemoryToBuffer(int Tracker, out byte[] Buffer, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.SaveTrackerMemoryToBuffer(HTracker Tracker, byte Buffer[]);
```

**Parameters:**

- **Tracker** - handle of the tracker to save.
- **Buffer** - pointer to the buffer to which the tracker memory will be saved.
- **MaxSizeInBytes** - amount of memory allocated for the output buffer, in bytes.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output buffer.

**Python Syntax:**

```python
def Tracker.GetMemory() -> bytes;

def Tracker.ToBytes() -> bytes;
```

**Return Value:**

The *bytes* objects containing tracker memory.

---

<a id="fsdk_loadtrackermemoryfrombuffer-function"></a>
## FSDK_LoadTrackerMemoryFromBuffer Function

Loads the memory of a tracker from a buffer. Note that tracker parameters, along with its face tracking state, are not loaded. See the Saving and Loading Tracker Memory section for details.

**C++ Syntax:**

```cpp
int FSDK_LoadTrackerMemoryFromBuffer(HTracker * Tracker, const unsigned char * Buffer);
```

**Delphi Syntax:**

```pascal
function FSDK_LoadTrackerMemoryFromBuffer(Tracker: PHTracker; var Buffer): integer;
```

**C# Syntax:**

```csharp
int FSDK.LoadTrackerMemoryFromBuffer(ref int Tracker, byte[] Buffer);
```

**Java and Android Syntax:**

```java
int FSDK.LoadTrackerMemoryFromBuffer(HTracker Tracker, byte Buffer[]);
```

**Parameters:**

- **Tracker** - pointer to store the handle of a loaded tracker.
- **Buffer** - pointer to the buffer from which to load the tracker memory.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_BAD_FILE_FORMAT if the file has unsupported format. Returns FSDKE_UNSUPPORTED_FILE_VERSION if the file was saved with Luxand FaceSDK of an unsupported version.

**Python Syntax:**

```python
def FSDK.LoadTrackerMemoryFromBuffer(buffer: bytes) -> Tracker;

@staticmethod
def Tracker.FromMemory(buffer: bytes) -> Tracker;

@staticmethod
def Tracker.FromBytes(buffer: bytes) -> Tracker;
```

**Return Value:**

New Tracker objects loaded from a *buffer*.

---

<a id="fsdk_gettrackeridscount-function"></a>
## FSDK_GetTrackerIDsCount Function

Returns the number of persons known to the tracker.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerIDsCount(HTracker Tracker, long long * Count);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerIDsCount(Tracker: HTracker; Count: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerIDsCount(ref int Tracker, ref long Count);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerIDsCount(HTracker Tracker, long Count[]);
```

**Parameters:**

- **Tracker** - pointer to store the handle of a tracker.
- **Count** - pointer to the buffer to which to store the count of IDs.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetTrackerIDsCount(tracker: Tracker) -> int;

def Tracker.GetIDsCount() -> int;
```

**Return Value:**

The Count of persons.

---

<a id="fsdk_gettrackerallids-function"></a>
## FSDK_GetTrackerAllIDs Function

Returns all IDs of persons known to the tracker. The number of IDs is defined by FSDK_GetTrackerIDsCount.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerAllIDs(HTracker Tracker, long long * IDList, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerAllIDs(Tracker: HTracker; IDList: PIDArray; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerAllIDs(int Tracker, out long[] IDList, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerAllIDs(HTracker Tracker, long IDList[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to get the list of identifiers.
- **IDList** - pointer to the array of 64-bit integer values that will store the list of identifiers.
- **MaxSizeInBytes** - amount of memory allocated for the output array.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetTrackerAllIDs(tracker: Tracker) -> List[int];

def Tracker.GetAllIDs() -> List[int];
```

**Return Value:**

The list of identifiers.

---

<a id="fsdk_gettrackerfaceidscountforid-function"></a>
## FSDK_GetTrackerFaceIDsCountForID Function

Returns the number of a person's FaceIDs by its ID.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFaceIDsCountForID(HTracker Tracker, long long ID, long long * Count);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFaceIDsCountForID(Tracker: HTracker; ID: int64; Count: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFaceIDsCountForID(ref int Tracker, long ID, ref long Count);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerFaceIDsCountForID(HTracker Tracker, long ID, long Count[]);
```

**Parameters:**

- **Tracker** - pointer to store the handle of a loaded tracker.
- **ID** - identifier of a person for which to return the number of FaceIDs.
- **Count** - pointer to the 64-bit integer value that will store the number of identifiers.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetTrackerFaceIDsCountForID(tracker: Tracker, ID: int) -> int;

def Tracker.GetFaceIDsCountForID(ID: int) -> int;
```

**Return Value:**

The Count of FaceIDs.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_gettrackerfaceidsforid-function"></a>
## FSDK_GetTrackerFaceIDsForID Function

Returns all FaceIDs of a person with given ID.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFaceIDsForID(HTracker Tracker, long long ID, long long * FaceIDList, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFaceIDsForID(Tracker: HTracker; ID: int64; IDList: PIDArray; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFaceIDsForID(int Tracker, long ID, out long[] IDList, long MaxSizeInBytes);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerFaceIDsForID(HTracker Tracker, long ID, long IDList[], long MaxSizeInBytes);
```

**Parameters:**

- **Tracker** - handle of the tracker in which to get the list of similar identifiers.
- **ID** - identifier of a person for which to return the list of FaceIDs.
- **IDList** - pointer to the array of 64-bit integer values that will store the list of identifiers.
- **MaxSizeInBytes** - amount of memory allocated for the output array.

**Return Value:**

Returns FSDKE_OK if successful. Returns FSDKE_INSUFFICIENT_BUFFER_SIZE if there is not enough room to store the output string; however, the output string still fills up all the space available.

**Python Syntax:**

```python
def FSDK.GetTrackerFaceIDsForID(tracker: Tracker, ID: int) -> List[int];

def Tracker.GetFaceIDsForID(ID: int) -> List[int];
```

**Return Value:**

The list of identifiers.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_gettrackeridbyfaceiid-function"></a>
## FSDK_GetTrackerIDByFaceIID Function

Returns the person's ID by its FaceID.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerIDByFaceID(HTracker Tracker, long long FaceID, long long * ID);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerIDByFaceID(Tracker: HTracker; FaceID: int64; ID: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerIDByFaceID(ref int Tracker, long FaceID, ref long ID);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerIDByFaceID(HTracker Tracker, long FaceID, long ID[]);
```

**Parameters:**

- **Tracker** - pointer to store the handle of a loaded tracker.
- **FaceID** - identifier of a person's FaceID for which to return the ID of a person.
- **ID** - pointer to the 64-bit integer value that will store the ID of a person.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetTrackerIDByFaceID(tracker: Tracker, FaceID: int) -> int;

def Tracker.GetIDByFaceID(FaceID: int) -> int;
```

**Return Value:**

The ID of a person.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_gettrackerfacetemplate-function"></a>
## FSDK_GetTrackerFaceTemplate Function

This function is used to extract a template from the tracker database for a given FaceID of a person.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFaceTemplate(HTracker Tracker, long long FaceID, FSDK_FaceTemplate * FaceTemplate);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFaceTemplate(Tracker: HTracker; FaceID: int64; FaceTemplate: PFSDK_FaceTemplate): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFaceTemplate(ref int Tracker, long FaceID, out byte[] FaceTemplate);
```

**Java Syntax:**

```java
int FSDK.GetTrackerFaceTemplate(HTracker Tracker, long FaceID, FSDK_FaceTemplate.ByReference FaceTemplate);
```

**Android Syntax:**

```java
int FSDK.GetTrackerFaceTemplate(HTracker Tracker, long FaceID, FSDK_FaceTemplate FaceTemplate);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceID** - the FaceID of a person for which to extract the face template stored in the tracker database.
- **FaceTemplate** - pointer to the FSDK_FaceTemplate structure, used to receive the face template.

**Return Value:**

Returns FSDKE_OK if successful. If the FaceID is not found, the function returns the FSDKE_FACEID_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.GetTrackerFaceTemplate(tracker: Tracker, FaceID: int) -> FaceTemplate;

def Tracker.GetFaceTemplate(FaceID: int) -> FaceTemplate;
```

**Return Value:**

The FaceTemplate object.

**Exceptions:**

FSDK.FaceIdNotFound

---

<a id="fsdk_trackercreateid-function"></a>
## FSDK_TrackerCreateID Function

This function creates new person in the tracker with given FaceTemplate and returns its new unique ID and FaceID.

**C++ Syntax:**

```cpp
int FSDK_TrackerCreateID(HTracker Tracker, FSDK_FaceTemplate * FaceTemplate, long long * ID, long long * FaceID);
```

**Delphi Syntax:**

```pascal
function FSDK_TrackerCreateID(Tracker: HTracker; FaceTemplate: PFSDK_FaceTemplate; ID: PInt64; FaceID: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.TrackerCreateID(ref int Tracker, ref byte[] FaceTemplate, ref long ID, ref long FaceID);
```

**Java Syntax:**

```java
int FSDK.TrackerCreateID(HTracker Tracker, FSDK_FaceTemplate.ByReference FaceTemplate, long ID[], long FaceID[]);
```

**Android Syntax:**

```java
int FSDK.TrackerCreateID(HTracker Tracker, FSDK_FaceTemplate FaceTemplate, long ID[], long FaceID[]);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceTemplate** - pointer to the FSDK_FaceTemplate structure to place it in the tracker database.
- **ID** - the ID of newly added person.
- **FaceID** - the FaceID of newly added person.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.TrackerCreateID(tracker: Tracker, FaceID: int) -> Tuple[int]; # (ID, FaceID)

def Tracker.CreateID(FaceID: int) -> Tuple[int]; # (ID, FaceID)
```

**Return Value:**

The tuple (ID, FaceID).

---

<a id="fsdk_addtrackerfacetemplate-function"></a>
## FSDK_AddTrackerFaceTemplate Function

This function adds new FaceTemplate to the existing person with ID.

**C++ Syntax:**

```cpp
int FSDK_AddTrackerFaceTemplate(HTracker Tracker, long long ID, FSDK_FaceTemplate * FaceTemplate, long long * FaceID);
```

**Delphi Syntax:**

```pascal
function FSDK_AddTrackerFaceTemplate(Tracker: HTracker; ID: int64; FaceTemplate: PFSDK_FaceTemplate; FaceID: PInt64): integer;
```

**C# Syntax:**

```csharp
int FSDK.AddTrackerFaceTemplate(ref int Tracker, long ID, ref byte[] FaceTemplate, ref long FaceID);
```

**Java Syntax:**

```java
int FSDK.AddTrackerFaceTemplate(HTracker Tracker, long ID, FSDK_FaceTemplate.ByReference FaceTemplate, long FaceID[]);
```

**Android Syntax:**

```java
int FSDK.AddTrackerFaceTemplate(HTracker Tracker, long ID, FSDK_FaceTemplate FaceTemplate, long FaceID[]);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **ID** - the ID of existing person.
- **FaceTemplate** - pointer to the FSDK_FaceTemplate structure to place it in the tracker database.
- **FaceID** - the pointer to receive new FaceID of face template for the person.

**Return Value:**

Returns FSDKE_OK if successful. If the ID is not found, the function returns the FSDKE_ID_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.AddTrackerFaceTemplate(tracker: Tracker, ID: int, faceTemplate: FaceTemplate) -> int;

def Tracker.AddFaceTemplate(ID: int, faceTemplate: FaceTemplate) -> int;
```

**Return Value:**

The FaceID of newly added face template.

**Exceptions:**

FSDK.IdNotFound

---

<a id="fsdk_deletetrackerface-function"></a>
## FSDK_DeleteTrackerFace Function

This function removes the face template with given FaceID from the tracker. The person will be removed from the tracker if it has no face templates anymore.

**C++ Syntax:**

```cpp
int FSDK_DeleteTrackerFace(HTracker Tracker, long long FaceID);
```

**Delphi Syntax:**

```pascal
function FSDK_DeleteTrackerFace(Tracker: HTracker; FaceID: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.DeleteTrackerFace(ref int Tracker, long FaceID);
```

**Java Syntax:**

```java
int FSDK.DeleteTrackerFace(HTracker Tracker, long FaceID);
```

**Android Syntax:**

```java
int FSDK.DeleteTrackerFace(HTracker Tracker, long FaceID);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceID** - the FaceID of existing person for which to remove the face template.

**Return Value:**

Returns FSDKE_OK if successful. If the FaceID is not found, the function returns the FSDKE_FACEID_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.DeleteTrackerFace(tracker: Tracker, FaceID: int);

def Tracker.DeleteFace(FaceID: int);
```

**Exceptions:**

FSDK.FaceIdNotFound

---

<a id="fsdk_gettrackerfaceimage-function"></a>
## FSDK_GetTrackerFaceImage Function

This function returns Image of a face with given FaceID.

**C++ Syntax:**

```cpp
int FSDK_GetTrackerFaceImage(HTracker Tracker, long long FaceID, HImage * Image);
```

**Delphi Syntax:**

```pascal
function FSDK_GetTrackerFaceImage(Tracker: HTracker; FaceID: int64; Image: PHImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetTrackerFaceImage(ref int Tracker, long FaceID, ref int Image);
```

**Java and Android Syntax:**

```java
int FSDK.GetTrackerFaceImage(HTracker Tracker, long FaceID, HImage Image);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceID** - the FaceID of existing face template for which to extract an image.
- **Image** - the pointer to HImage for receiving the newly created image handle.

**Return Value:**

Returns FSDKE_OK if successful. If the FaceID is not found, the function returns the FSDKE_FACEID_NOT_FOUND code. If face template has no image, the code FSDKE_FACEIMAGE_NOT_FOUND is returned.

**Python Syntax:**

```python
def FSDK.GetTrackerFaceImage(tracker: Tracker, FaceID: int) -> Image;

def Tracker.GetFaceImage(FaceID: int) -> Image;
```

**Return Value:**

An image of face template.

**Exceptions:**

FSDK.FaceIdNotFound

---

<a id="fsdk_settrackerfaceimage-function"></a>
## FSDK_SetTrackerFaceImage Function

This function places an Image for a face with given FaceID to the tracker. The Image should be 96x96 pixels in grey mode (8 bpp). If an image with this FaceID is already exists, it is replaced by the new one.

**C++ Syntax:**

```cpp
int FSDK_SetTrackerFaceImage(HTracker Tracker, long long FaceID, HImage Image);
```

**Delphi Syntax:**

```pascal
function FSDK_SetTrackerFaceImage(Tracker: HTracker; FaceID: int64; Image: HImage): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetTrackerFaceImage(ref int Tracker, long FaceID, int Image);
```

**Java and Android Syntax:**

```java
int FSDK.SetTrackerFaceImage(HTracker Tracker, long FaceID, HImage Image);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceID** - the FaceID of existing face template for which to save an image.
- **Image** - handle to the image to be stored in the tracker.

**Return Value:**

Returns FSDKE_OK if successful. If the FaceID is not found, the function returns the FSDKE_FACEID_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.SetTrackerFaceImage(tracker: Tracker, FaceID: int, image: Image);

def Tracker.SetFaceImage(FaceID: int, image: Image);
```

**Exceptions:**

FSDK.FaceIdNotFound

---

<a id="fsdk_deletetrackerfaceimage-function"></a>
## FSDK_DeleteTrackerFaceImage Function

This function removes an image from the tracker with given FaceID.

**C++ Syntax:**

```cpp
int FSDK_DeleteTrackerFaceImage(HTracker Tracker, long long FaceID);
```

**Delphi Syntax:**

```pascal
function FSDK_DeleteTrackerFaceImage(Tracker: HTracker; FaceID: int64): integer;
```

**C# Syntax:**

```csharp
int FSDK.DeleteTrackerFaceImage(ref int Tracker, long FaceID);
```

**Java and Android Syntax:**

```java
int FSDK.DeleteTrackerFaceImage(HTracker Tracker, long FaceID);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceID** - the FaceID of existing face template for which to remove an image.

**Return Value:**

Returns FSDKE_OK if successful. If the FaceID is not found, the function returns the FSDKE_FACEID_NOT_FOUND code.

**Python Syntax:**

```python
def FSDK.DeleteTrackerFaceImage(tracker: Tracker, FaceID: int);

def Tracker.DeleteFaceImage(FaceID: int);
```

**Exceptions:**

FSDK.FaceIdNotFound

---

<a id="fsdk_trackermatchfaces-function"></a>
## FSDK_TrackerMatchFaces Function

The function compares the FaceTemplate with all templates stored in the tracker, finds the IDs of individuals that match the Threshold, and writes them to a buffer IDSimilarity structures in descending order of probability, starting with the highest. The number of found IDs is placed in the Count field.

**C++ Syntax:**

```cpp
typedef struct {
    long long ID;
    float similarity;
} IDSimilarity;

int FSDK_TrackerMatchFaces(HTracker Tracker, FSDK_FaceTemplate * FaceTemplate, float Threshold, IDSimilarity * Buffer, long long * Count, long long MaxSizeInBytes);
```

**Delphi Syntax:**

```pascal
IDSimilarity = record
    ID: int64;
    Similarity: single;
end;
PIDSimilarity = ^IDSimilarity;

function FSDK_TrackerMatchFaces(Tracker: HTracker; FaceTemplate: PFSDK_FaceTemplate; Threshold: single; Buffer: PIDSimilarity; Count: PInt64; MaxSizeInBytes: int64): integer;
```

**C# Syntax:**

```csharp
public struct IDSimilarity {
    public long ID;
    public float similarity;
}

int FSDK.TrackerMatchFaces(ref int Tracker, ref byte[] FaceTemplate, float Threshold, out IDSimilarity[] Buffer, out long Count, long MaxSizeInBytes);
```

**Java and Android Syntax:**

The class IDSimilarity contains the following fields:

```java
public long ID;
public float similarity;
```

```java
int FSDK.TrackerMatchFaces(HTracker Tracker, FSDK_FaceTemplate.ByReference FaceTemplate, ...);
```

**Parameters:**

- **Tracker** - pointer to the handle of a tracker.
- **FaceTemplate** - pointer to the FSDK_FaceTemplate structure using it for comparison with all templates stored in the tracker.
- **Threshold** - the similarity threshold for matching.
- **Buffer** - the pointer to buffer of IDSimilarity structures to receive comparison results.
- **Count** - pointer to the 64-bit integer value that will store the number of found IDs.
- **MaxSizeInBytes** - amount of memory allocated for the output array.

**Return Value:**

Returns FSDKE_OK if successful. If the ID is not found, the function returns the FSDKE_ID_NOT_FOUND code.

**Python Syntax:**

```python
class IDSimilarity(ctypes.Structure):
    _fields_ = ("ID", c_longlong), ("similarity", c_float)

def FSDK.TrackerMatchFaces(tracker: Tracker, faceTemplate: FaceTemplate, threshold: float, maxCount: int = 5) -> List[IDSimilarity];

def Tracker.MatchFaces(ID: int, faceTemplate: FaceTemplate, threshold: float, maxCount: int = 5) -> int;
```

**Return Value:**

The FaceID of newly added face template.

**Exceptions:**

FSDK.IdNotFound

<a id="multi-core-support"></a>
# Multi-Core Support

The following FaceSDK functions use multiple CPU cores, thus speeding up the calculations:

```text
FSDK_DetectEyes
FSDK_DetectEyesInRegion
FSDK_DetectFace
FSDK_DetectMultipleFaces
FSDK_DetectFacialFeatures
FSDK_DetectFacialFeaturesInRegion
FSDK_GetFaceTemplate
FSDK_GetFaceTemplateInRegion
FSDK_GetFaceTemplateUsingFeatures
FSDK_GetFaceTemplateUsingEyes
FSDK_FeedFrame
FSDK_TrackerMatchFaces
```

By default, these functions use all available processor cores. To get the number of processor cores used, call the FSDK_GetNumThreads function. To limit the number of processor cores used, call the FSDK_SetNumThreads function. Calling FSDK_SetNumThreads(1) will disable multi-core support.

Note that each of these functions forks into a number of threads on each call. It is not recommended to use nested parallelism when calling these functions; if you need nested parallelism, you may limit the number of threads with the [FSDK_SetNumThreads](#fsdk_setnumthreads-function) function. For example, if your application runs in several threads, and each thread executes [FSDK_DetectFace](#fsdk_detectface-function) (which uses all available cores), this is acceptable; however, if each thread forks into several threads, each executing [FSDK_DetectFace](#fsdk_detectface-function), this could potentially reach the limit of resources available.

It is safe to use extensions for parallel computation (like OpenMP) with the above FaceSDK functions, if they are executed from a single thread. For example, the following C++ sample code is acceptable:

```cpp
#pragma omp parallel for
for (int i = 0; i < 100; i++)
    FSDK_DetectFace(...);
```

However, if your application forks into multiple threads, it is not recommended to execute the above FaceSDK functions within OpenMP statements in such threads. If you must, consider limiting the number of cores used by FaceSDK with the [FSDK_SetNumThreads](#fsdk_setnumthreads-function) function.

---

<a id="fsdk_getnumthreads-function"></a>
## FSDK_GetNumThreads Function

Retrieves the number of processor cores used by FaceSDK.

**C++ Syntax:**

```cpp
int FSDK_GetNumThreads(int * Num);
```

**Delphi Syntax:**

```delphi
function FSDK_GetNumThreads(Num: PInteger): integer;
```

**C# Syntax:**

```csharp
int FSDK.GetNumThreads(ref int Num);
```

**Java and Android Syntax:**

```java
int FSDK.GetNumThreads(int Num[]);
```

**Parameters:**

*Num* is the pointer to an integer value to receive the number of threads used by FaceSDK.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.GetNumThreads() -> int
```

**Return Value:**

The number of processor cores used by FaceSDK.

---

<a id="fsdk_setnumthreads-function"></a>
## FSDK_SetNumThreads Function

Sets the number of processor cores to be used by FaceSDK. If you set the number of cores to 1, support for multiple cores will be disabled, and the SDK will use only a single processor core.

**C++ Syntax:**

```cpp
int FSDK_SetNumThreads(int Num);
```

**Delphi Syntax:**

```delphi
function FSDK_SetNumThreads(Num: integer): integer;
```

**C# Syntax:**

```csharp
int FSDK.SetNumThreads(int Num);
```

**Java and Android Syntax:**

```java
int FSDK.SetNumThreads(int Num);
```

**Parameters:**

*Num* - the number of cores to be used by FaceSDK.

**Return Value:**

Returns FSDKE_OK if successful.

**Python Syntax:**

```python
def FSDK.SetNumThreads(num: int)
```

**Return Value:**

None.

---

<a id="performance-optimization-guide"></a>
## Performance Optimization Guide

<a id="optimizing-for-high-throughput-scenarios"></a>
### Optimizing for High-Throughput Scenarios

When processing large numbers of images or video streams, consider these strategies to maximize throughput:

**Thread configuration for batch processing (C++, OpenMP):**

```cpp
// For batch image processing across multiple threads:
// Limit FaceSDK to 1-2 cores per call to allow parallel processing
int totalCores;
FSDK_GetNumThreads(&totalCores);

// Use half the cores for FaceSDK, leaving the rest for your application threads
FSDK_SetNumThreads(totalCores / 2);

// Now process images in parallel using your own thread pool
#pragma omp parallel for
for (int i = 0; i < imageCount; i++) {
    HImage img;
    FSDK_LoadImageFromFile(&img, filenames[i]);
    FSDK_FaceTemplate tmpl;
    int err = FSDK_GetFaceTemplate(img, &tmpl);
    if (err == FSDKE_OK) {
        // Store template...
    }
    FSDK_FreeImage(img);
}
```

<a id="tuning-face-detection-for-different-scenarios"></a>
### Tuning Face Detection for Different Scenarios

Use [FSDK_SetFaceDetectionParameters](#fsdk_setfacedetectionparameters-function) to optimize detection for your specific use case:

**Webcam / real-time detection (prioritize speed):**

```cpp
// Fast detection for real-time video at close range
FSDK_SetFaceDetectionParameters(false, false, 128);
FSDK_SetNumThreads(1);  // Single-threaded for lowest latency per frame
```

**High-resolution photo processing (prioritize accuracy):**

```cpp
// Thorough detection for high-res images
FSDK_SetFaceDetectionParameters(true, true, 512);
// Use all available cores for maximum throughput
int numCores;
FSDK_GetNumThreads(&numCores);
FSDK_SetNumThreads(numCores);
```

**Thermal / infrared camera images:**

```cpp
// Thermal cameras produce lower-contrast images
// Use lower detection threshold and higher resolution
FSDK_SetFaceDetectionParameters(false, false, 384);
FSDK_SetFaceDetectionThreshold(3);  // Lower threshold for low-contrast images
```

<a id="performance-tips"></a>
### Performance Tips

- **Single-threaded per call is faster for real-time video** — set `FSDK_SetNumThreads(1)` when processing one frame at a time, as thread overhead can exceed the parallelism benefit for a single operation.
- **Multi-threaded is faster for batch processing** — use all cores when processing many images in a single FaceSDK call or when each call processes a large image.
- **Reduce InternalResizeWidth for speed** — lower values (e.g., 128) detect faces faster but may miss faces that are small relative to the image. Use higher values (e.g., 512) only when detecting distant or small faces.
- **Free images promptly** — call [FSDK_FreeImage](#fsdk_freeimage-function) as soon as processing is complete to keep memory usage low during batch operations.
- **Avoid nested parallelism** — do not use OpenMP or other parallelism inside threads that already call multi-core FaceSDK functions. Instead, limit FaceSDK threads with [FSDK_SetNumThreads](#fsdk_setnumthreads-function) and manage parallelism at the application level.

<a id="thread-safety"></a>
# Thread Safety

This chapter describes using FaceSDK in applications that execute FaceSDK functions from multiple threads. If your program runs in a single thread (by default, this happens in almost all environments), you can skip this chapter.

Most FaceSDK functions are safe for multithreaded operations. The functions not guaranteed to be thread-safe are:

```text
FSDK_Initialize
FSDK_Finalize
FSDK_ActivateLibrary
FSDK_GetLicenseInfo
FSDK_GetHardware_ID
FSDK_SetNumThreads
```

When working with cameras in multiple threads on Windows platforms, make sure that each thread calls the [FSDK_InitializeCapturing](#fsdk_initializecapturing-function) function and the [FSDK_FinalizeCapturing](#fsdk_finalizecapturing-function) function when the thread is done. The following functions are thread safe (on all supported platforms) given that no different threads are simultaneously accessing the same camera handle:

```text
FSDK_GetVideoFormatList
FSDK_FreeVideoFormatList
FSDK_SetVideoFormat
FSDK_OpenVideoCamera
FSDK_CloseVideoCamera
FSDK_GrabFrame
```

The following functions set global parameters that have effect on each thread:

```text
FSDK_SetFaceDetectionParameters
FSDK_SetFaceDetectionThreshold
FSDK_SetJpegCompressionQuality
FSDK_SetCameraNaming
FSDK_SetHTTPProxy
FSDK_SetNumThreads
```

Note that HImage is safe only for multiple simultaneous reads or single write. Do not read from (e.g. with [FSDK_DetectFace](#fsdk_detectface-function)) and write to (e.g. with [FSDK_FreeImage](#fsdk_freeimage-function)) the same HImage handle at one time.

For more information on thread safety of Tracker API, see the Thread Safety section in the [Tracker API](#tracker-api-face-recognition-and-tracking-in-video-streams) chapter.

<a id="migration"></a>
# Migration

<a id="migration-from-facesdk-82-to-facesdk-83"></a>
## Migration from FaceSDK 8.2 to FaceSDK 8.3

<a id="net-wrapper"></a>
### .NET wrapper

Use new .NET wrapper. Please read the migration guide.

Key Changes:

- Classes are no longer nested (FSDK.Cam -> Camera, FSDK.CImage -> CImage)
- Better parameter semantics (ref -> in/out or removed)
- New high-level classes: Tracker, Camera, CImage (standalone)
- Improved error handling with CheckForError()
- Better XML documentation and modern C# patterns
- New features: Tracker enhancements, GetVersionInfo(), better IDisposable

Class mapping:

| Old | New |
|-----|-----|
| FSDKCam (static) | Camera (static methods) / FSDK |
| FSDK.Cam | Luxand.Camera |
| FSDK.CImage | Luxand.CImage |
| | Tracker (NEW, recommended) |

Key signature changes:

1. Parameter Modifiers:

OLD: ref (used for everything)

NEW: in (input), out (output), or no modifier (simple input)

Examples:

- ref TFacePosition -> in TFacePosition
- ref float similarity -> out float similarity
- ref string cameraName -> string cameraName (no modifier)
- ref byte[] template -> byte[] template (no modifier)

2. Common Method Changes:

- DetectFace(img, ref pos) -> DetectFace(img, out pos)
- DetectEyesInRegion(img, ref pos, ...) -> DetectEyesInRegion(img, in pos, ...)
- MatchFaces(ref t1, ref t2, ref sim) -> MatchFaces(t1, t2, out sim)
- GetMatchingThresholdAtFAR(f, ref t) -> GetMatchingThresholdAtFAR(f, out t)
- CreateTracker(ref handle) -> CreateTracker(out handle)
- FeedFrame(t, c, i, ref cnt, out ids) -> FeedFrame(t, c, i, out cnt, out ids)

Camera changes:

OLD:

```csharp
FSDKCam.InitializeCapturing();
string[] cameras;
int count;
FSDKCam.GetCameraList(out cameras, out count);
string camName = cameras[0];
FSDK.Cam camera = new FSDK.Cam(ref camName);
FSDK.CImage frame = camera.GrabFrame();
```

NEW:

```csharp
Camera.InitializeCapturing();
string[] cameras = Camera.GetCameraList();
Camera camera = new Camera(cameras[0]);
CImage frame = camera.GrabFrame();
```

NEW (Better with using Luxand):

```csharp
using (Camera camera = new Camera(Camera.GetCameraList()[0])) {
    using (CImage frame = camera.GrabFrame()) {
        // Process frame
    }
}
```

Image handling:

OLD:

```csharp
int handle = 0;
FSDK.LoadImageFromFile(ref handle, "image.jpg");
FSDK.CImage img = new FSDK.CImage(handle);
FSDK.TFacePosition pos = new FSDK.TFacePosition();
FSDK.DetectFace(img.ImageHandle, ref pos);
```

NEW:

```csharp
CImage img = new CImage("image.jpg");
FSDK.TFacePosition pos = img.DetectFace();
```

Detection changes:

OLD:

```csharp
FSDK.TFacePosition[] faces;
int detected = 0;
FSDK.DetectMultipleFaces(imgHandle, ref detected, out faces, 256*24);
FSDK.TPoint[] features;
FSDK.DetectFacialFeaturesInRegion(imgHandle, ref facePos, out features);
```

NEW:

```csharp
FSDK.TFacePosition[] faces = img.DetectMultipleFaces();
FSDK.TPoint[] features = img.DetectFacialFeaturesInRegion(facePos);
```

Template matching changes:

OLD:

```csharp
byte[] t1, t2;
FSDK.GetFaceTemplate(img1, out t1);
FSDK.GetFaceTemplateInRegion(img2, ref pos, out t2);
float similarity = 0;
FSDK.MatchFaces(ref t1, ref t2, ref similarity);
```

NEW:

```csharp
byte[] t1 = image1.GetFaceTemplate();
byte[] t2 = image2.GetFaceTemplateInRegion(pos);
FSDK.MatchFaces(t1, t2, out float similarity);
```

Tracker changes:

OLD:

```csharp
int tracker = 0;
FSDK.CreateTracker(ref tracker);
FSDK.SetTrackerParameter(tracker, "RecognizeFaces", "true");
long count = 0;
long[] ids;
FSDK.FeedFrame(tracker, 0, imgHandle, ref count, out ids, 1024);
FSDK.TFacePosition pos = new FSDK.TFacePosition();
FSDK.GetTrackerFacePosition(tracker, 0, ids[0], ref pos);
FSDK.FreeTracker(tracker);
```

NEW (Option 1 - Direct FSDK):

```csharp
int tracker;
FSDK.CreateTracker(out tracker);
FSDK.SetTrackerParameter(tracker, "RecognizeFaces", "true");
long count;
long[] ids;
FSDK.FeedFrame(tracker, 0, imgHandle, out count, out ids, 1024);
FSDK.TFacePosition pos;
FSDK.GetTrackerFacePosition(tracker, 0, ids[0], out pos);
FSDK.FreeTracker(tracker);
```

NEW (Option 2 - Tracker class, RECOMMENDED):

```csharp
using (Tracker tracker = new Tracker()) {
    tracker.SetParameter("RecognizeFaces", "true");
    long[] ids;
    tracker.FeedFrame(image, out ids);
    foreach (long id in ids) {
        FSDK.TFacePosition pos = tracker.GetFacePosition(0, id);
        string name = tracker.GetName(id);
    }
}
```

New tracker features:

New methods available only in new wrapper:

- tracker.GetIDsCount() / GetAllIDs()
- tracker.GetFaceIDsForID(id) / GetIDByFaceID(faceId)
- tracker.GetFaceTemplate(faceId)
- tracker.CreateID(template, out id, out faceId)
- tracker.AddFaceTemplate(id, template, out faceId)
- tracker.DeleteFace(faceId)
- tracker.GetFaceImage(faceId) / SetFaceImage(faceId, img)
- tracker.MatchFaces(template, threshold, out results)

Error handling:

OLD:

```csharp
int res = FSDK.LoadImageFromFile(ref handle, file);
if (res != FSDK.FSDKE_OK)
    throw new Exception("Error: " + res);
```

NEW (Manual):

```csharp
int res = FSDK.LoadImageFromFile(out handle, file);
if (res != FSDK.FSDKE_OK)
    throw new Exception("Luxand FaceSDK Error Number " + res);
```

NEW (Recommended):

```csharp
int res = FSDK.LoadImageFromFile(out handle, file);
FSDK.CheckForError(res);
```

NEW (High-level classes):

```csharp
CImage img = new CImage(file); // Throws on error automatically
```

Essential Steps:

- Replace all FSDK.Cam references with Luxand.Camera
- Replace all FSDK.CImage references with Luxand.CImage
- Remove 'ref' from camera name parameters
- Change 'ref' to 'in' for TFacePosition input parameters
- Change 'ref' to 'out' for similarity, threshold, count outputs
- Remove 'ref' from template arrays (use plain arrays)
- Update tracker creation: CreateTracker(ref h) -> CreateTracker(out h)
- Update FeedFrame: FeedFrame(..., ref count, ...) -> FeedFrame(..., out count, ...)
- Update GetTrackerFacePosition: (..., ref pos) -> (..., out pos)
- Consider using high-level Tracker class instead of manual handle
- Use CheckForError() for error handling

Recommended Improvements:

- Use 'using' statements for Camera, CImage, Tracker
- Use CImage methods (DetectFace, GetFaceTemplate) instead of FSDK static methods
- Use Tracker class methods instead of direct FSDK tracker calls
- Explore new v8.3 features (GetAllIDs, MatchFaces, etc.)

---

<a id="migration-from-facesdk-81-to-facesdk-82"></a>
## Migration from FaceSDK 8.1 to FaceSDK 8.2

Use iBeta Certified Liveness Add-on for enhanced passive liveness detection, available in the samples\ibeta liveness add-on directory.

The minimum supported iOS version is 12.0.

The minimum supported Linux versions are CentOS/RHEL 8 (glibc 2.28+).

---

<a id="migration-from-facesdk-72-721-to-facesdk-80-81"></a>
## Migration from FaceSDK 7.2, 7.2.1 to FaceSDK 8.0, 8.1

For compatibility with the latest Xcode versions the libfsdk-static.a and libfsdk-static_64.a libraries for iOS have been joined into a single library libfsdk-static.a.

.NET applications now use FaceSDK.NET.dll built from the samples\advanced\.NET wrapper source, so adding the appropriate binary file (facesdk.dll, libfsdk.dylib or libfsdk.so) is required.

The minimum supported iOS version is 9.0.

The minimum supported Android version is 5.0.

The minimum supported Windows version is Windows 7.

The minimum supported macOS version is 10.13.

---

<a id="migration-from-facesdk-71-to-facesdk-72-721"></a>
## Migration from FaceSDK 7.1 to FaceSDK 7.2, 7.2.1

InternalResizeWidth parameter values larger than 512 are now supported to allow for the detection of even small faces on high-resolution images.

JPEG images are now automatically rotated on load using the EXIF data.

The minimum supported Linux versions are CentOS/RHEL 7. Older Linux versions are no longer supported.

The minimum supported Windows version is Windows Vista.

---

<a id="migration-from-facesdk-651-to-facesdk-70-71"></a>
## Migration from FaceSDK 6.5.1 to FaceSDK 7.0, 7.1

<a id="face-detection"></a>
### Face Detection

Version 7.0 introduces a new face detection engine, which is more accurate when detecting faces that are rotated out of plane, blurred, backlit, or in low lighting conditions.

The new engine does not currently support *InternalResizeWidth* parameter values larger than 512 (see the FSDK_SetFaceDetectionParameters chapter). If you are detecting small faces on high-resolution images with large *InternalResizeWidth* values, consider splitting such images into parts.

When the *InternalResizeWidth* is set to 512, faces that are heavily cropped and occupy almost all of the image (such as when a face is too close to the camera) could be detected less often than when smaller *InternalResizeWidth* values are used. However, large *InternalResizeWidth* values are not necessary when detecting such faces. In this case, consider setting the *InternalResizeWidth* to 256 or less.

As the new engine uses color information, the face detection rates on grayscale images could be lower (especially on small faces).

You may find that small faces are detected less often. In this case, try increasing the *InternalResizeWidth* value, as the internal meaning of *InternalResizeWidth* has changed in the engine.

<a id="template-format-changes"></a>
### Template format changes

Version 7.0 improves the accuracy of the FSDK_GetFaceTemplate and FSDK_MatchFaces functions. Templates are extracted in such a way that the false acceptance rates are decreased when matching blurred, low-lit, and out-of-plane faces.

The accuracy of matching templates extracted by previous FaceSDK versions is unchanged. To enjoy the increased accuracy, consider re-extracting your templates from the source images by using version 7.0.

If you are using Tracker API with the *KeepFaceImages* parameter set to true, the Tracker facial appearances will be automatically re-extracted when the Tracker memory, saved with versions 6.5 or 6.5.1, is loaded (using the FSDK_LoadTrackerMemoryFromFile or FSDK_LoadTrackerMemoryFromBuffer functions). This may take some time, depending on the size of your Tracker memory.

<a id="removal-of-libstdc-dependency-on-ios"></a>
### Removal of libstdc++ dependency on iOS

FaceSDK 7.0 for iOS has removed the dependency on the libstdc++ library to increase compatibility with Xcode 10. FaceSDK sample applications for iOS are no longer using libstdc++. To switch from using libstdc++ to using libc++ in your Xcode project, visit Build Settings - C++ Standard Library. iOS 5.x and 6.x are no longer supported.

---

<a id="migration-from-facesdk-65-to-facesdk-651"></a>
## Migration from FaceSDK 6.5 to FaceSDK 6.5.1

The 6.5.1 version improves the extraction of facial templates from images taken under very low lighting conditions. As the 6.5 version might produce higher false acceptance rates on such images, it is recommended that you re-extract your facial templates from the source pictures using the 6.5.1 version.

If you were using Tracker API with the KeepFaceImages parameter set to true, the Tracker facial appearances will be automatically re-extracted when the Tracker memory, saved with the 6.5 version, is loaded (using the FSDK_LoadTrackerMemoryFromFile or FSDK_LoadTrackerMemoryFromBuffer functions). This may take some time, depending on the size of your Tracker memory. If you were using the Tracker API in very low light, it is recommended that you start the Tracker memory from scratch and re-enroll your subjects.

---

<a id="migration-from-facesdk-63-631-64-to-facesdk-65"></a>
## Migration from FaceSDK 6.3, 6.3.1, 6.4 to FaceSDK 6.5

<a id="template-format-changes"></a>
### Template format changes

The 6.5 version improves face matching accuracy. It achieves a true acceptance rate of 99.83% and a false acceptance rate of 0.1% for the NIST FRGC protocol, ROC1 (compared to the 93.9% true acceptance rate achieved by the 6.4 version).

To achieve the accuracy increase, it was necessary to change the format of the face template (the FSDK_FaceTemplate structure). The size of the face template was decreased to 1040 bytes. To migrate to the 6.5 version and start using the new face templates, you need to update the Luxand FaceSDK interface header files in your project (see [Using FaceSDK with Programming Languages](#using-facesdk-with-programming-languages)) and rebuild your application. If you were relying on the size of the old face template structure (13324 bytes), for example, while saving it to a database, you need to change this value to 1040.

As the new face template is not compatible with the face template from previous versions, you need to re-extract the templates for every face in your database (with the FSDK_GetFaceTemplate, FSDK_GetFaceTemplateInRegion, or FSDK_GetFaceTemplateUsingFeatures functions) from the source pictures. As the template format may change again in future versions, it is recommended that you store both the original face images and their templates in the database.

The 6.5 version increased its matching accuracy, because of its more sophisticated models. However, such models require more calculations. The speed of template extraction is now lower than in the 6.4 version. This means that on slow devices, you may get lower frame rates when extracting face templates, with either the FSDK_GetFaceTemplate, FSDK_GetFaceTemplateInRegion, or FSDK_GetFaceTemplateUsingFeatures functions.

<a id="template-matching"></a>
### Template matching

The 6.5 version substantially increases the speed of face matching on most platforms. You are unlikely to require any code changes to adapt to this.

<a id="tracker-api-changes"></a>
### Tracker API changes

Since the template format has changed, the Tracker memory from previous Luxand FaceSDK versions is not compatible with the 6.5 version. This means you cannot load the Tracker memory saved with Luxand FaceSDK 6.4 (and earlier) using the FSDK_LoadTrackerMemoryFromFile or FSDK_LoadTrackerMemoryFromBuffer functions. To migrate to the 6.5 version, you need to start a new Tracker memory file and enroll all your subjects again.

If it is not possible for you to regenerate the templates or start a new Tracker memory, please contact our support at https://www.luxand.com/support/.

To make the transition to new template formats easier when using Tracker API, we added the KeepFaceImages parameter. When set to true (which is the default value), it will store the original facial images in the Tracker memory. If the template format changes in the new version of Tracker API, you will be able to convert your previous Tracker memory to the new template format automatically, so you won't need to reenroll your subjects. If you don't like the original facial images to be stored in the Tracker memory, you need to explicitly set this parameter to false. See the [Storing original facial images](#storing-original-facial-images) section for more details.

As the speed of template extraction has decreased compared to the 6.4 version, you may get lower frame rates when the RecognizeFaces parameter is set to true. In older versions, it was recommended that higher frame rates were preferable, in order that Tracker API could collect more facial appearances of a person per unit of time, which positively affected the accuracy (see the [Tuning for Optimal Performance](#tuning-for-optimal-performance) chapter). However, the Tracker API in the 6.5 version is less affected by the frame rate, because it has more robust face matching. Even if you're processing about 1 frame per second on a slow device, it is usually enough for Tracker API to efficiently recognize persons; even with that frame rate, you're likely to get much higher recognition rates than in the 6.4 version with higher frame rates.

Note that if your RecognizeFaces is set to false when using Tracker API (for example, when you only detect faces or facial features), your frame rate will not decrease.

The *RecognitionPrecision* parameter now has no effect and is not recommended for use.

---

<a id="migration-from-facesdk-62-to-facesdk-63-631-64"></a>
## Migration from FaceSDK 6.2 to FaceSDK 6.3, 6.3.1, 6.4

The 6.3 version increases minimal OS version requirements. Applications developed with Luxand FaceSDK 6.3 will not support any Windows versions earlier than Windows XP SP3 or Windows 2003 SP2 and will not support any macOS versions earlier than 10.7.

If you are using Luxand FaceSDK with Microsoft .NET, note that FaceSDK.NET.dll now requires .NET 4.0 or higher. You need to redistribute Microsoft Visual C++ Redistributable for Visual Studio 2017 with your application.

If you are using an older version of .NET (for example, 2.0, 3.0 or 3.5), you must switch to the component available in the source code form in the samples\advanced\.NET wrapper directory. Note that this component is actually a wrapper for facesdk.dll that is linked dynamically, so facesdk.dll must be redistributed with the application that uses this wrapper. The LiveRecognition sample includes projects for Microsoft C# 2005/2008 and Visual Basic .NET 2005/2008 that are using this wrapper.

The LiveFacialFeatures, GenderRecognition and ExpressionRecognition samples were updated to be compatible with iOS 11. If your code was based on these samples, update your code accordingly. You need to implement the changes by moving the code that creates the cache from drawFrameWithWidth to onGLInit. These changes were implemented in the TrackingViewController.mm file of the samples.

---

<a id="migration-from-facesdk-60-601-61-to-facesdk-62"></a>
## Migration from FaceSDK 6.0, 6.0.1, 6.1 to FaceSDK 6.2

The 6.2 version adds 4 new facial feature points (numbered 66 to 69), detecting 70 facial features instead of 66 in the previous release. The following constants are added:

FSDKP_FACE_CONTOUR14, FSDKP_FACE_CONTOUR15, FSDKP_FACE_CONTOUR16, FSDKP_FACE_CONTOUR17.

The numbering of the 66 facial features detected previously was not changed. It means that the new numbering is backwards compatible with the previous numbering. When migrating to the 6.2 or 6.3 version, make sure that you are using the new header files (or wrappers), since the FSDK_Features type now contains 4 more points.

The FSDK_GetFaceTemplateUsingFeatures function still employs only the first 66 facial features.

The performance of retrieving live video in the LiveFacialFeatures sample for iOS and Android is increased. If you were using this sample code in your project, consider replacing the corresponding parts of your code to increase the performance of your app.

---

<a id="migration-from-facesdk-50-501-to-facesdk-60-601-61"></a>
## Migration from FaceSDK 5.0, 5.0.1 to FaceSDK 6.0, 6.0.1, 6.1

Important changes for users migrating to Luxand FaceSDK 6.0, 6.01 or 6.1 from the 5.0 or 5.0.1 versions:

The FSDK_GetFaceTemplate and FSDK_GetFaceTemplateInRegion functions now detect facial features with the same accuracy as the FSDK_DetectFacialFeatures function. The accuracy of face recognition is now the same regardless of whether you call FSDK_GetFaceTemplate/FSDK_GetFaceTemplateInRegion or first detect facial features and then pass them to the FSDK_GetFaceTemplateUsingFeatures function.

The recognition accuracy of Tracker API when RecognitionPrecision=1 is now independent of the values of the DetectFacialFeatures or DetectGender parameters.

The FacialFeatureJitterSuppression parameter of Tracker API now allows for better facial feature smoothing; however, its default setting may consume more processor resources. You may set its value to 0 if you need to consume fewer resources.

---

<a id="migration-from-facesdk-40-to-facesdk-50-501"></a>
## Migration from FaceSDK 4.0 to FaceSDK 5.0, 5.0.1

Important changes for users migrating to Luxand FaceSDK 5.0 or 5.0.1 from the 4.0 version:

The function FSDK_GetFaceTemplateUsingFeatures is no longer deprecated. The function expects that the coordinates of all facial features are detected. If you are passing just the coordinates of eye centers (detected with FSDK_DetectEyes, FSDK_DetectEyesInRegion) to the function, call FSDK_GetFaceTemplateUsingEyes instead.

The format of the face template has changed. The size of the template is now 13324 bytes. If you have stored face templates in a database, you must recreate them from the original photos by calling the FSDK_GetFaceTemplate or FSDK_GetFaceTemplateInRegion functions.

The FSDK_MatchFaces function now returns an error when the template has an invalid format or when the formats of the templates are not supported (that is, when face templates was created with an unsupported version of Luxand FaceSDK).

If you were calling FSDK_GetFaceTemplate or FSDK_GetFaceTemplateInRegion, you may find that they consume more time. This is because these functions extract face templates with higher accuracy. If you need higher performance, replace these calls with FSDK_DetectEyes or FSDK_DetectEyesInRegion, and call FSDK_GetFaceTemplateUsingEyes. See the Face Matching section for details.

On the other hand, if you were detecting eyes and then passing their coordinates to FSDK_GetFaceTemplateUsingEyes, you need to replace this call together with the detection of eye centers to the FSDK_GetFaceTemplate or FSDK_GetFaceTemplateInRegion function to achieve the higher accuracy available in the 5.0 version.

---

<a id="migration-from-facesdk-30-to-facesdk-40"></a>
## Migration from FaceSDK 3.0 to FaceSDK 4.0

Recommendations on how to migrate from version 3.0 to version 4.0 are included.

1. The 4.0 version introduces a new high-quality algorithm for facial feature detection. The new version detects 66 facial features (see the Detected Facial Features chapter).
2. The 4.0 version enhances the accuracy of inner facial feature (nose, eyes, and mouth) detection. To make this enhancement possible, facial feature points of the upper part of the head were removed. The following facial feature points (and their corresponding constants) were removed:

   FSDKP_FACE_CONTOUR3, FSDKP_FACE_CONTOUR4, FSDKP_FACE_CONTOUR5, FSDKP_FACE_CONTOUR6, FSDKP_FACE_CONTOUR7, FSDKP_FACE_CONTOUR8, FSDKP_FACE_CONTOUR9, FSDKP_FACE_CONTOUR10, FSDKP_FACE_CONTOUR11

   If you were using some of these features, you may calculate their approximate positions by relying on the coordinates of other facial features.

3. You may find that FaceSDK consumes more CPU resources than the previous version. The SDK uses all available CPU cores for face detection and recognition functions, achieving higher speed. If you need the SDK to use just a single core (as in the previous version), use the FSDK_SetNumThreads function.
4. The following functions are deprecated and will not be supported in the future Luxand FaceSDK versions: FSDK_GetFaceTemplateUsingFeatures.

---

<a id="migration-from-facesdk-20-to-facesdk-30"></a>
## Migration from FaceSDK 2.0 to FaceSDK 3.0

This section tells about changes in FaceSDK 3.0 as compared to FaceSDK 2.0. There are also recommendations on how to migrate from version 2.0 to version 3.0.

1. As version 3.0 has introduced a new enhanced face recognition algorithm, the format of a template changed as well. Now it is enough to detect only eye centers, rather than all features to build a template. If your application used to detect facial features and then created a template using detected features, now the feature detection stage can be skipped or replaced by detection of eye centers (i.e. FSDK_DetectFacialFeatures can be replaced by FSDK_DetectEyes). The size of a template was reduced to 16384 bytes. If your application used a database of saved templates, it is necessary to recreate these templates using source images.
2. New version introduces new functions for quick detection of eye centers - FSDK_DetectEyes and FSDK_DetectEyesInRegion. These functions are recommended for use if it is necessary to detect eye centers in real time.
3. The meaning of similarity returned by FSDK_MatchFaces function has changed. Now similarity is approximately equal to the probability that templates belong to one and the same person. More information on this topic can be found in Face Matching chapter.
4. The new FSDK_SetCameraNaming function is added. It determines what the FSDK_GetCameraList function returns - either the list of camera names available in the system, or the list of unique device paths of these cameras. (It may be required if two similar webcams of the same manufacturer are plugged in to the computer.)
5. Camera management functions are included into facesdk.dll. If you used camera management in your applications, you may remove facesdkcam.dll and header files related to facesdkcam.
6. .NET wrapper does not require facesdk.dll. The camera management functions are also included into FaceSDK.NET.dll (but they are still located in class FSDKcam). Now the wrapper is located in the directories \bin\win32\ for 32-bit applications and \bin\win64\ for 64-bit applications.
7. The following functions have been removed from the library and will not be supported: FSDK_LocateFace, FSDK_LocateFacialFeatures, FSDK_ExtractFaceImage.
8. The following functions are deprecated and will not be supported in the future Luxand FaceSDK versions: FSDK_GetFaceTemplateUsingFeatures.

<a id="error-codes"></a>
# Error Codes

The FaceSDK library defines the following error codes:

| Error Name | Value |
|---|---|
| FSDKE_OK | 0 |
| FSDKE_FAILED | -1 |
| FSDKE_NOT_ACTIVATED | -2 |
| FSDKE_OUT_OF_MEMORY | -3 |
| FSDKE_INVALID_ARGUMENT | -4 |
| FSDKE_IO_ERROR | -5 |
| FSDKE_IMAGE_TOO_SMALL | -6 |
| FSDKE_FACE_NOT_FOUND | -7 |
| FSDKE_INSUFFICIENT_BUFFER_SIZE | -8 |
| FSDKE_UNSUPPORTED_IMAGE_EXTENSION | -9 |
| FSDKE_CANNOT_OPEN_FILE | -10 |
| FSDKE_CANNOT_CREATE_FILE | -11 |
| FSDKE_BAD_FILE_FORMAT | -12 |
| FSDKE_FILE_NOT_FOUND | -13 |
| FSDKE_CONNECTION_CLOSED | -14 |
| FSDKE_CONNECTION_FAILED | -15 |
| FSDKE_IP_INIT_FAILED | -16 |
| FSDKE_NEED_SERVER_ACTIVATION | -17 |
| FSDKE_ID_NOT_FOUND | -18 |
| FSDKE_ATTRIBUTE_NOT_DETECTED | -19 |
| FSDKE_INSUFFICIENT_TRACKER_MEMORY_LIMIT | -20 |
| FSDKE_UNKNOWN_ATTRIBUTE | -21 |
| FSDKE_UNSUPPORTED_FILE_VERSION | -22 |
| FSDKE_SYNTAX_ERROR | -23 |
| FSDKE_PARAMETER_NOT_FOUND | -24 |
| FSDKE_INVALID_TEMPLATE | -25 |
| FSDKE_UNSUPPORTED_TEMPLATE_VERSION | -26 |
| FSDKE_CAMERA_INDEX_DOES_NOT_EXIST | -27 |
| FSDKE_PLATFORM_NOT_LICENSED | -28 |
| FSDKE_TENSORFLOW_NOT_INITIALIZED | -29 |
| FSDKE_PLUGIN_NOT_LOADED | -30 |
| FSDKE_PLUGIN_NO_PERMISSION | -31 |
| FSDKE_FACEID_NOT_FOUND | -32 |
| FSDKE_FACEIMAGE_NOT_FOUND | -33 |
| FSDKE_IBETA_INITIALIZATION_ERROR | -200 |

<a id="library-information"></a>
# Library Information

The FaceSDK library uses:

- TensorFlow-Lite В© Google, LLC;
- OpenVINO В© Intel Corporation;
- tbb В© Intel Corporation;
- libjpeg-turbo (copyright by Miyasaka Masaru, TigerVNC and VirtualGL projects);
- libcurl В© Daniel Stenberg;
- libpng В© Glenn Randers-Pehrson;
- easybmp В© The EasyBMP Project ([http://easybmp.sourceforge.net](http://easybmp.sourceforge.net/));
- RSA Data Security, Inc. MD5 Message-Digest Algorithm.
