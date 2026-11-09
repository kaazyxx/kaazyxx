# CLAUDE.md — PSX CAPTURE

## 1. PROJECT IDENTITY

Project name: PSX Capture

Project type: Native Windows PlayStation 5 Remote Play client.

Main objective:
Develop a real Windows application capable of connecting to a PlayStation 5 over a local network, receiving its Remote Play stream, decoding video and audio, and displaying it with the lowest practical latency.

This is a real software project, not a UI mockup or a simulated application.

## 2. TARGET HARDWARE

Development and target environment:

* Windows 10 / Windows 11
* NVIDIA RTX 5070
* Ethernet and Wi-Fi connectivity
* 1080p target resolution
* 60 FPS stable target
* 120 Hz display support where possible

Important:
A 120 Hz display does not mean the PS5 Remote Play stream provides 120 native FPS. Never fabricate frames or advertise unsupported performance.

## 3. CORE DEVELOPMENT PRINCIPLES

Always prioritize in this order:

1. Functional correctness
2. Connection stability
3. Low latency
4. Video and audio quality
5. Resource efficiency
6. User experience
7. Visual polish

Never sacrifice stability for artificial benchmark improvements.

Never claim a feature is implemented unless it actually works and has been tested.

## 4. TECHNOLOGY STACK

Preferred technologies:

* C++ for the core engine
* CMake for build management
* Qt 6 for the Windows interface
* Chiaki-ng / libchiaki for Remote Play compatibility
* FFmpeg for media processing where appropriate
* NVIDIA NVDEC for hardware video decoding where supported
* DirectX 11/12 for rendering
* WASAPI for audio output
* Windows APIs for system integration

Technology decisions must be justified.

Before integrating a dependency:

* Check its maintenance status.
* Check Windows compatibility.
* Check its license.
* Check its build requirements.
* Check whether an existing implementation already provides the required functionality.

Respect AGPL-3.0 and all other applicable licenses. Do not copy or redistribute third-party code without respecting its terms.

## 5. PROJECT ARCHITECTURE

Keep the code modular.

Suggested structure:

```
PSX-Capture/
├── CLAUDE.md
├── CMakeLists.txt
├── README.md
├── src/
│   ├── main.cpp
│   ├── core/
│   ├── remoteplay/
│   ├── video/
│   ├── audio/
│   ├── network/
│   ├── controller/
│   ├── recording/
│   └── statistics/
├── ui/
│   ├── dashboard/
│   ├── player/
│   └── settings/
├── resources/
│   ├── icons/
│   ├── fonts/
│   └── styles/
├── tests/
├── dependencies/
├── scripts/
└── installer/
```

You may improve this structure when necessary, but keep modules separated and maintainable.

## 6. REMOTE PLAY ENGINE

The Remote Play engine is the most important component.

Requirements:

* PS5 discovery where supported.
* Console registration and pairing.
* Secure credential handling.
* Session initialization.
* Video stream reception.
* Audio stream reception.
* Controller input support.
* Connection state monitoring.
* Session termination.
* Automatic recovery from recoverable errors.

Use a maintained and compatible Remote Play implementation whenever possible.

Never simulate a successful connection.

Never bypass Sony authentication or security protections.

## 7. VIDEO ENGINE

Implement:

* Hardware decoding when supported.
* NVIDIA NVDEC integration where compatible.
* Software decoding fallback.
* Efficient frame delivery.
* Minimal unnecessary memory copies.
* Frame timing measurements.
* Correct synchronization.
* Fullscreen rendering.
* Resolution reporting.

Measure:

* Incoming FPS.
* Displayed FPS.
* Decode time.
* Render time.
* Frame queue depth.
* Dropped frames.

Never confuse monitor refresh rate with source frame rate.

## 8. AUDIO ENGINE

Implement:

* PS5 audio reception.
* WASAPI output.
* Audio device selection.
* Volume control.
* Audio/video synchronization.
* Proper cleanup when disconnecting.

Avoid unnecessary audio buffering.

## 9. NETWORK ENGINE

Support:

* Ethernet.
* Wi-Fi.
* Network interface selection where practical.
* Connection quality monitoring.
* Packet loss reporting.
* Reconnection handling.
* Network diagnostics.

Prefer a direct local network connection.

Do not introduce external relays or cloud servers unless explicitly required.

Do not confuse network latency with total input-to-display latency.

## 10. CONTROLLER SUPPORT

Implement:

* DualSense support where compatible.
* USB controller support.
* Bluetooth support where practical.
* Button mapping.
* Input forwarding.
* Connection status.

Do not promise advanced DualSense features until they are verified.

## 11. RECORDING SYSTEM

Implement:

* MP4 recording.
* Screenshot capture.
* Recording folder selection.
* Recording status indicator.
* Audio recording.
* Configurable recording quality.
* Safe file finalization after stopping.

Recording must not destabilize live playback.

## 12. STATISTICS AND DIAGNOSTICS

Provide a live statistics panel displaying:

* Source FPS.
* Display FPS.
* Stream resolution.
* Network latency estimate.
* Decode time.
* Render time.
* Packet loss.
* Dropped frames.
* CPU usage.
* GPU usage when available.

Clearly distinguish measured values from estimates.

Include structured application logs.

Never invent measurements.

## 13. UI / UX DESIGN SYSTEM

Visual direction:

* Premium dark interface.
* Deep black background.
* Anthracite surfaces.
* Subtle purple accent.
* Restrained glassmorphism.
* Clean typography.
* Consistent spacing.
* Smooth transitions.
* Minimal visual noise.

Avoid:

* Excessive gradients.
* Excessive glow.
* Overused neon effects.
* Unnecessary animations.
* Generic AI-generated dashboard aesthetics.
* Cluttered settings screens.

The interface should feel like a professionally developed Windows gaming application.

### Main screens

Dashboard:

* PS5 connection status.
* Connect / Disconnect.
* Console information.
* Network status.
* Recent sessions.

Player:

* Large video preview.
* Fullscreen mode.
* Audio controls.
* FPS counter.
* Connection statistics.

Settings:

* Video configuration.
* Decoder selection.
* Audio devices.
* Network settings.
* Controller configuration.
* Recording configuration.

## 14. CODING STANDARDS

* Use clear C++ naming conventions.
* Prefer RAII.
* Avoid memory leaks.
* Avoid unnecessary global variables.
* Use appropriate thread synchronization.
* Handle errors explicitly.
* Keep functions focused.
* Avoid giant source files.
* Document complex technical decisions.
* Keep dependencies organized.
* Never commit secrets or credentials.
* Avoid hardcoded absolute paths.

## 15. BUILD AND TEST RULES

Compile regularly.

After every significant module:

1. Build the project.
2. Fix compilation errors.
3. Run relevant tests.
4. Check logs.
5. Verify resource cleanup.

Tests must cover:

* Connection failure.
* Connection success when a real console is available.
* Disconnection.
* Network interruption.
* Decoder fallback.
* Audio device changes.
* Recording start and stop.
* Repeated connection sessions.

Do not report unperformed tests as successful.

## 16. SECURITY

* Never store credentials in plaintext.
* Use Windows Credential Manager or an appropriate secure storage mechanism.
* Validate configuration inputs.
* Avoid unsafe shell execution.
* Do not expose pairing credentials in logs.
* Handle sensitive data carefully.

## 17. DEVELOPMENT WORKFLOW

Before modifying code:

* Inspect the existing project.
* Understand its architecture.
* Identify dependencies.
* Check the current build state.

When implementing a feature:

* Explain the intended implementation briefly.
* Modify the necessary files.
* Build the project.
* Run tests.
* Report the result.

Do not rewrite working modules unnecessarily.

Do not silently remove existing functionality.

Do not create placeholder implementations for core features.

If a technical limitation prevents implementation, explain it honestly and propose a realistic alternative.

## 18. CURRENT DEVELOPMENT PRIORITIES

Priority 1:
Build a working Windows project and integrate the Remote Play engine.

Priority 2:
Connect to a real PS5 and receive its video stream.

Priority 3:
Implement stable video and audio playback.

Priority 4:
Optimize decoding and rendering.

Priority 5:
Implement the custom interface.

Priority 6:
Add recording, statistics and installer.

## 19. FINAL RULE

The ultimate objective is to deliver a stable, native Windows PS5 Remote Play application.

Always prioritize real functionality over appearance.

Always prioritize measured performance over marketing claims.

Always preserve project stability.

Never pretend that something works when it does not.
