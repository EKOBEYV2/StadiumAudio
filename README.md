# README - StadiumAudio iOS App

## Project Overview
**StadiumAudio** is a professional, high-performance iOS application designed to transform audio listening over Bluetooth, AUX, or AirPlay into an immersive **STADIUM / CONCERT HALL** acoustic experience.

---

## Technical Highlights
- **Frameworks**: Swift 5.9+, SwiftUI, `AVFoundation`, `AVAudioEngine`, `Accelerate/vDSP`, `CoreAudioKit`.
- **Signal Chain Architecture**:
  `Input (AVAudioPlayerNode) -> 3-Band Parametric EQ -> vDSP Stereo Widener -> Early Reflections & Algorithmic Reverb -> Delay/Echo -> Dry/Wet Crossfader -> Safety Peak Limiter -> Output Node`
- **Output Route Tracking**: Dynamically detects connected **Bluetooth** (including car head units), **AUX / Headphones**, **AirPlay**, and **Built-in Speakers**.
- **Compliant AUv3 Extension**: Includes an official Audio Unit v3 (AUv3) Effect extension (`aufx/revb`) allowing live processing inside host applications like GarageBand, Logic Pro, and AUM.
- **Strict iOS Security Compliance**: iOS sandboxing strictly prevents third-party apps from intercepting global system audio (e.g., Spotify or YouTube Music). The app clearly communicates this limitation in the UI and provides two official Apple-supported solutions: local file DSP player (MP3, WAV, AAC, M4A) and AUv3 plugin integration.

---

## File Structure
- `StadiumAudio/App/StadiumAudioApp.swift`: Main app entry point & Audio Session configuration.
- `StadiumAudio/Models/ReverbPreset.swift`: Model containing presets (STADIUM, CONCERT HALL, ARENA, LIVE CONCERT, BIG ROOM, CATHEDRAL, CLUB, SMALL ROOM, VOCAL HALL) with official Stadium values.
- `StadiumAudio/Models/AudioTrack.swift`: Track model and `AudioRouteInfo` definitions.
- `StadiumAudio/AudioEngine/DSPChain.swift`: Low-latency real-time DSP pipeline.
- `StadiumAudio/AudioEngine/StereoWidenerNode.swift`: Mid/Side stereo widening using `Accelerate/vDSP`.
- `StadiumAudio/AudioEngine/AudioRouteManager.swift`: Handles `AVAudioSession` route change & interruption notifications.
- `StadiumAudio/AudioEngine/AudioFilePlayerManager.swift`: Timeline scrubber, track loader, and Files app importer.
- `StadiumAudio/ViewModels/MainViewModel.swift`: Reactive MVVM coordinator.
- `StadiumAudio/Views/MainView.swift`: Modern, dark-themed cockpit interface.
- `StadiumAudioAUv3/`: Complete Audio Unit v3 plugin code (`StadiumAudioAUv3AudioUnit.swift`, `AudioUnitViewController.swift`, `Info.plist`).

---

## How to Build in Xcode
1. Open Xcode and create a new iOS App project named `StadiumAudio`.
2. Add all files in the `StadiumAudio` directory to the main application target.
3. Add a new target: **Audio Unit Extension** named `StadiumAudioAUv3` and attach the files in `StadiumAudioAUv3`.
4. Ensure the **Background Modes** capability is enabled for **Audio, AirPlay, and Picture in Picture**.
5. Build and run on an iOS Device or Simulator!
