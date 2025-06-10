# NouraSDK Android

NouraSDK is an Android library for building interactive AI-powered experiences in Android applications.

**Current Version: 0.2.4**

## Overview

NouraSDK provides a pre-built chat interface and AI capabilities that can be easily integrated into any Android application using Jetpack Compose.

## Prerequisites

- Android Studio Arctic Fox (2020.3.1) or later
- Android API 26+ (Android 8.0)
- Kotlin 1.8.0 or later
- Gradle 8.0 or later

## Installation

### Using GitHub Pages Maven Repository

Add the repository and dependency to your app's `build.gradle.kts`:

```kotlin
repositories {
    google()
    mavenCentral()
    maven { url = uri("https://sarj-ai.github.io/noura-sdk-android/") }
}

dependencies {
    implementation("ai.sarj:nourasdk:0.2.4")
}
```

### Alternative: Direct AAR

Download the AAR directly:
1. Download `nourasdk-0.2.4.aar` from the [releases](./releases/) directory
2. Place it in your `app/libs/` directory  
3. Add to your `build.gradle.kts`:

```kotlin
dependencies {
    implementation(files("libs/nourasdk-0.2.4.aar"))
    
    // Required dependencies
    implementation("com.airbnb.android:lottie-compose:6.4.1")
}
```

## SDK Integration

### 1. Configure the SDK

Initialize the SDK in your Application or Activity:

```kotlin
import ai.sarj.nourasdk.NouraSDKManager
import ai.sarj.nourasdk.NouraSDKCallback
import ai.sarj.nourasdk.NouraSDKError

// Create a callback handler to receive events and errors
class AppNouraCallbackHandler : NouraSDKCallback {
    override fun onError(error: NouraSDKError) {
        Log.e("NouraSDK", "Error: ${error.message}")
        // Handle SDK errors in your app
    }
    
    override fun onChatStarted() {
        Log.d("NouraSDK", "Chat session started")
        // Log events to your analytics system
    }
    
    override fun onChatEnded() {
        Log.d("NouraSDK", "Chat session ended")
    }
}

// Configure the SDK with your API key and callback handler
NouraSDKManager.shared.configure(
    apiUrl = "YOUR_API_URL",
    apiKey = "YOUR_API_KEY",
    context = this,
    callback = AppNouraCallbackHandler()
)
```

### 2. Present the Chat Interface

#### Option A: Launch in New Activity

```kotlin
// Open chat in a new activity
NouraSDKManager.shared.openChat(this)
```

#### Option B: Embed in Compose UI

```kotlin
import ai.sarj.nourasdk.NouraSDKChatContent

@Composable
fun MyScreen() {
    NouraSDKChatContent(
        onBackPressed = { /* Handle back navigation */ }
    )
}
```

## Usage Notes

- The SDK provides a pre-built chat interface using Jetpack Compose
- Supports both English and Arabic localization with RTL layout
- Includes Lottie animations for enhanced user experience
- Requires a valid API key for authentication
- Minimum deployment target is Android API 26 (Android 8.0)

---

© 2025 Sarj AI. All rights reserved.
