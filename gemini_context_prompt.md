# Gemini Context Setter + Feature Prompts

## Phase 1: Context Setter Prompt

Paste this into a new chat with Gemini in Android Studio. This tells the AI exactly what "St. Ann's Connect" is, so it stops guessing.

Copy and paste this block:

```
System Role: You are a Senior Android Developer expert in Kotlin, Jetpack Compose, and Firebase.

Project Overview:

I am building a school management app called "St. Ann's Connect" for St. Ann's A U P School, Nileshwar.

The app has two user roles with distinct dashboards:

Parents: Need to track bus locations, pay fees via WhatsApp receipts, view exams, reports, and access resources like Samagra/Sahitham.

Teachers: Need an AI-powered student dashboard ("Ente Kutty"), a library book scanner, and tools to update tasks.

Technical Stack:

Language: Kotlin
UI: Jetpack Compose (Material3 Design System)
Navigation: androidx.navigation
Backend: Firebase Firestore (Database) & Firebase Auth.
AI: Google Gemini API (Client-side integration).

Data Structure (Mental Model):

users collection: { uid, role: "parent"|"teacher", name, classId }
students collection: { id, name, parentId, busFeeStatus, teacherNotes }

Current Status:

I have a basic MainActivity with a Login Screen and Navigation set up. Now I need to build the specific feature screens.

Please keep all code concise, use modern best practices, and explain complex logic simply.
```

## Phase 2: Feature-Specific Prompts

Once you have sent the prompt above, use these specific prompts to generate the code for each complex feature. Do them one by one.

### Feature A: The "WhatsApp Bus Receipt" (For Teachers)

This generates the logic to save data to Firebase AND open WhatsApp automatically.

Prompt:

```
Write a Jetpack Compose screen called BusFeeCollectionScreen.Requirements:

Display a list of students (mock data for now).

When a teacher selects a student, show an input field for "Amount Received" (default 500).

A button "Confirm & Send Receipt".

Logic: When clicked, it should trigger an Android Intent to open WhatsApp.

The message should be pre-filled: "Dear Parent, Receipt for [Student Name]. Amount [Amount] received for Bus Fee. Balance: 0. - St. Ann's School."

Include the necessary Intent code to handle cases where WhatsApp is not installed.
```

### Feature B: The "AI Ente Kutty" Dashboard (For Teachers)

This moves the logic we built in the React prototype into Android.

Prompt:

```
Write a Jetpack Compose screen called StudentAIDashboard.Requirements:

A text area for "Teacher Scribbles" (Raw notes).

A button "Generate AI Report".

Gemini Integration: Create a suspend function callGemini(prompt: String) that makes a POST request to the Gemini API URL.

Prompt Logic: The prompt sent to AI should be: "Refine these teacher notes into a professional report card comment: [User Input]".

Display the AI result in a clean card below the button.

Note: I will provide the API Key later, just create a placeholder variable for it.
```

### Feature C: The "Parent Dashboard" (WebView Features)

For Samagra, Wiki, and Chapters.

Prompt:

```
Write a reusable Compose function called WebViewScreen(url: String).Requirements:

It should take a URL as a parameter.

Use AndroidView to render a standard WebView.

Enable JavaScript in the WebView settings (needed for Samagra).

Show a loading spinner (CircularProgressIndicator) while the page loads.

Show me how to call this screen from the Parent Dashboard when they click "Samagra Resources".
```

### Feature D: The "Library Scanner" (Camera)

This is the advanced feature.

Prompt:

```
I need a screen called LibraryScannerScreen for teachers.Requirements:

Use CameraX library to show a camera preview.

A button "Capture Book Cover".

When captured, convert the ImageProxy or Bitmap to Base64.

AI Logic: Prepare a function to send this Base64 image to Gemini Pro Vision API with the prompt "Extract the Book Title and Author from this image in JSON format."
```

## How to use these?

Don't do it all at once. Build the WhatsApp Receipt first. It provides immediate value (saving money on printing).

Copy-Paste Errors: If Gemini gives you code that has red lines (errors), hover over the error and click "Alt+Enter" (Option+Enter on Mac) to import libraries.

Manifest File: Remember, for WhatsApp and Camera to work, you will need to ask Gemini: "What permissions do I need to add to my AndroidManifest.xml for this feature?"

Start with Phase 1 to set the context, then do Feature A. Let me know when you are ready for the code review!
