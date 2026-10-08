# PRD.md — VisionMate AI

## 1. Project Overview

**VisionMate AI** is an AI-powered visual assistant prototype designed to help users understand their surroundings through a camera and spoken feedback. The initial prototype uses a laptop/browser camera. The architecture must allow the camera source to later be replaced by a smart-spectacles camera connected through USB, Wi-Fi, Bluetooth, Raspberry Pi, or a phone.

The system combines:

- Live camera capture
- YOLO object detection
- OCR using Tesseract or EasyOCR
- Vision-capable AI for scene understanding
- Speech-to-text for voice commands
- Text-to-speech for spoken responses
- Safety-mode obstacle awareness
- A professional Streamlit interface

**Important limitation:** Safety Mode is an assistive prototype. It must never be presented as guaranteed collision avoidance, navigation, medical advice, or a certified safety system.

## 2. Project Vision

Create a practical, accessible AI assistant that can transform visual information into concise spoken information, making a user's surroundings easier to understand.

## 3. Business Objective

The objective is to demonstrate a hackathon-quality assistive AI prototype that integrates computer vision, OCR, multimodal AI, speech recognition, and text-to-speech in one workflow.

Commercial claims, customer statistics, partnerships, certifications, pricing, and production safety guarantees are **To Be Decided**.

## 4. Problem Statement

People who have difficulty visually interpreting their surroundings may benefit from rapid access to information about objects, text, and scenes. Conventional camera applications expose raw visual information but do not automatically convert it into concise, useful spoken feedback.

VisionMate AI addresses this prototype problem by combining computer vision and voice interfaces.

## 5. Goals

1. Provide a usable live camera interface.
2. Detect common objects with YOLO.
3. Describe captured scenes using a vision-capable AI model.
4. Extract visible text using OCR.
5. Read extracted text aloud.
6. Accept voice questions and return image-aware answers.
7. Provide experimental obstacle warnings in Safety Mode.
8. Keep the camera layer replaceable so smart spectacles can be integrated later.
9. Provide clear system status and error feedback.
10. Maintain accessible, high-contrast, responsive UI.

## 6. Non-Goals

- Guaranteed collision avoidance.
- Autonomous navigation.
- Medical diagnosis.
- Certified assistive-device functionality.
- Facial recognition unless separately approved.
- Identification of private individuals.
- Production-grade smart-glasses hardware in the initial prototype.
- Invented statistics, testimonials, partners, or certifications.

## 7. Target Users

### Primary Persona — Accessibility User
Needs concise information about objects, text, and surroundings and benefits from voice-first interaction.

### Secondary Persona — Demonstration User
A judge, developer, student, or evaluator testing the prototype during a hackathon.

### Technical Persona — Developer
Needs modular interfaces for replacing the laptop camera with an external smart-spectacles camera and replacing AI/OCR/STT/TTS providers.

## 8. User Roles

| Role | Capabilities |
|---|---|
| User | Camera, object detection, scene description, OCR, voice assistant, Safety Mode |
| Developer | Configuration, provider replacement, debugging, deployment |
| System Administrator | To Be Decided; no separate admin dashboard is required by the current project scope |

No authentication or RBAC is required for the initial local/demo prototype unless the deployment environment later requires it.

## 9. User Journeys

### Object Detection
Open VisionMate → allow camera → camera connected → select Detect Objects → capture/process frame → YOLO inference → bounding boxes + labels + confidence → display result.

### Scene Description
Open camera → capture image → select Describe Scene → send image to vision AI → receive concise description → display description → optionally speak response.

### Read Text
Capture image → select Read Text → OCR extracts text → display extracted text → convert text to speech → play audio.

### Voice Assistant
Activate Ask VisionMate → speech-to-text → combine recognized question with current/captured image → vision AI response → display response → text-to-speech → audio output.

### Safety Mode
Enable Safety Mode → repeated camera analysis → object/obstacle detection → estimate proximity using available visual signals → display warning → issue spoken warning when configured. The interface must identify this as an assistive prototype.

## 10. User Stories

- As a user, I want to see the camera feed so I can frame a scene.
- As a user, I want to detect objects so I can understand what is around me.
- As a user, I want object labels and confidence scores.
- As a user, I want a short description of a scene.
- As a user, I want to extract text from an image.
- As a user, I want extracted text spoken aloud.
- As a user, I want to ask questions about what the camera sees.
- As a user, I want spoken responses.
- As a user, I want Safety Mode to warn me about detected obstacles.
- As a developer, I want the camera provider to be replaceable.
- As a developer, I want API keys stored outside source code.

## 11. Complete Website/Application Structure

The Streamlit application is primarily a single interactive application rather than a multi-page marketing website.

### Main Application
- Header/brand
- Live camera panel
- Feature controls
- Results panel
- Voice output indicator
- System status panel
- Safety disclaimer
- Error/status notifications

### Supporting Routes/Views Where Implemented
- Main application
- Privacy Policy — required if deployed publicly and data is processed
- Terms & Conditions — required if deployed publicly
- Custom error handling
- Thank-you/status view only if a future feedback/contact workflow is added

## 12. Navigation Structure

Primary navigation should remain simple:

**VisionMate AI → Camera → Describe Scene → Detect Objects → Read Text → Safety Mode → Ask VisionMate**

A sidebar may group controls without making the interface feel like an administration system.

## 13. Page-by-Page Requirements

### Main VisionMate Interface

**Purpose:** Central workspace for all visual-assistance features.

**Inputs:** Camera frames, captured image, selected feature, optional voice question.

**Expected Behavior:** Process the selected input using the appropriate pipeline and show a clear result.

**Outputs:** Detection results, OCR text, AI description/answer, safety warning, or audio feedback.

**Acceptance Criteria:**
- Camera permission and availability are clearly shown.
- Feature controls work only when required inputs are available.
- Processing states are visible.
- Errors are understandable.
- Results do not expose API keys or internal stack traces.

### Privacy Policy
Explain camera, image, audio, and API processing behavior accurately. Any retention period or third-party processing details must be **To Be Decided** unless defined by the final deployment.

### Terms & Conditions
Define appropriate use, prototype limitations, user responsibility, and safety limitations.

## 14. Functional Requirements

### FR-01 Live Camera

**Purpose:** Provide live visual input.

**User:** User.

**Inputs:** Laptop/browser camera.

**Expected Behavior:** Display live camera feed and provide capture control.

**Output:** Current frame/captured image.

**Acceptance Criteria:**
- Camera can be selected/initialized.
- Camera unavailable state is shown.
- Capture works.
- Camera resources are released appropriately.
- Camera abstraction allows future external camera adapters.

### FR-02 Object Detection

**Purpose:** Identify visible objects.

**User:** User.

**Inputs:** Captured/current image.

**Expected Behavior:** Run YOLO inference.

**Output:** Object labels, confidence values, and bounding boxes.

**Acceptance Criteria:**
- YOLO model loads successfully.
- Bounding boxes correspond to detections.
- Confidence values are shown.
- Low-confidence detections can be filtered using configuration.
- Inference errors are safely handled.

### FR-03 Scene Description

**Purpose:** Convert an image into a concise natural-language description.

**Inputs:** Captured image.

**Expected Behavior:** Send image to configured vision-capable AI provider.

**Output:** Short scene description.

**Acceptance Criteria:**
- API key is loaded from environment configuration.
- Image is encoded/transmitted securely.
- Timeout/error handling exists.
- The response is displayed and can be spoken.

### FR-04 OCR / Read Text

**Purpose:** Extract and vocalize visible text.

**Inputs:** Captured image.

**Expected Behavior:** OCR processes the image.

**Output:** Extracted text and optional speech.

**Acceptance Criteria:**
- OCR provider is configurable between Tesseract/EasyOCR.
- Empty OCR results are handled.
- Text is displayed clearly.
- TTS can read the extracted result.

### FR-05 Safety Mode

**Purpose:** Provide experimental warnings for detected nearby obstacles.

**Inputs:** Repeated camera frames.

**Expected Behavior:** Analyze frames continuously or at a configured interval and issue warnings for configured detection conditions.

**Output:** Visual and spoken warning.

**Acceptance Criteria:**
- Safety Mode can be enabled/disabled.
- Warning thresholds are configurable.
- Warning state is visually prominent.
- Voice warning is rate-limited to prevent repeated speech flooding.
- UI explicitly states that this is an assistive prototype and not guaranteed collision avoidance.

### FR-06 Voice Assistant

**Purpose:** Allow natural voice interaction.

**Inputs:** User speech and current/captured image.

**Expected Behavior:** STT → question processing → vision AI → TTS.

**Output:** Recognized question, AI response, spoken response.

**Acceptance Criteria:**
- Microphone permission failures are handled.
- STT failure is shown safely.
- AI receives the required image/question.
- TTS output can be triggered.
- No sensitive credentials appear in UI.

## 15. Forms and Inputs

The prototype has minimal forms:

| Input | Type | Validation |
|---|---|---|
| Camera source | Select/configuration | Supported source only |
| Detection confidence | Numeric | 0–1 |
| OCR engine | Select | Supported provider |
| AI provider/model | Configuration | Required if scene/voice AI is enabled |
| Voice question | Speech/text | Non-empty before submission |
| Safety warning interval | Numeric | Positive bounded value |

API keys must never be entered into a public UI form. They belong in environment variables/secrets.

## 16. CTA Requirements

Primary CTAs:

- **Describe Scene**
- **Detect Objects**
- **Read Text**
- **Safety Mode**
- **Ask VisionMate**
- **Capture**

CTAs must clearly indicate when processing is active.

## 17. Admin Requirements

No admin dashboard is required by the current prototype scope.

If a future cloud deployment requires administration, the admin architecture should be added only after requirements are defined.

## 18. Content Management

Static interface text should be stored in maintainable application modules/configuration rather than duplicated throughout the codebase.

Dynamic content management is not required.

## 19. Search/Filter Requirements

No search is required.

Object detections may be filtered by:
- Confidence threshold
- Optional object-class allowlist/denylist if later required

## 20. Authentication Requirements

Authentication is not required for the initial local/demo prototype.

If public multi-user deployment is introduced, authentication requirements become **To Be Decided** based on data handling and deployment needs.

## 21. Authorization/RBAC

No RBAC is required for the current prototype.

## 22. Database Requirements

A database is not required for core local processing.

Supabase PostgreSQL from the generic master stack is therefore **not required for the current VisionMate prototype** unless future requirements introduce persistent users, sessions, settings, feedback, analytics, or application records.

Do not create unnecessary tables or fake database functionality.

## 23. SEO Requirements

SEO is secondary because the product is primarily an interactive application. If publicly deployed:
- Page title: VisionMate AI
- Description must accurately describe the product.
- Open Graph metadata should be configured.
- `robots.txt` should be configured according to whether the app should be indexed.
- A sitemap is only required if there are indexable public pages.
- No unsupported accessibility or safety claims.

## 24. Accessibility Requirements

- High contrast.
- Large readable controls.
- Clear button labels.
- Keyboard-accessible controls where Streamlit permits.
- Avoid color-only status indicators.
- Visible focus/active states where supported.
- Screen-reader-friendly labels where supported.
- Spoken output must have visual text equivalents.
- Safety warnings must use text + visual emphasis + optional audio.
- Do not depend on audio alone for critical system status.

## 25. Responsive Requirements

The UI must work on:
- Desktop
- Laptop
- Tablet
- Mobile where browser camera/microphone support permits

Test:
- Camera panel scaling
- Button wrapping
- Result cards
- Text readability
- No unwanted horizontal overflow
- Audio controls
- Status indicators

## 26. Performance Requirements

- Avoid unnecessary full-resolution frame processing.
- Resize frames before inference when appropriate.
- Use model caching to avoid reloading YOLO on every interaction.
- Cache stable resources safely.
- Use asynchronous/background approaches where supported and useful.
- Limit Safety Mode processing frequency.
- Avoid sending unnecessary frames to external AI APIs.
- Compress/resize images before external transfer when quality permits.
- Display processing indicators.

## 27. Security Requirements

- Store API keys in environment variables/secrets.
- Never hardcode credentials.
- Never expose server-side credentials to the browser/UI.
- Validate uploaded/captured content.
- Limit image sizes.
- Use HTTPS for deployed applications.
- Use safe API timeouts.
- Avoid logging raw sensitive images/audio unnecessarily.
- Avoid exposing stack traces.
- Sanitize user-generated text where it is rendered as HTML.
- Use least privilege for external API credentials.
- Document third-party AI/OCR/STT/TTS data handling before public deployment.

## 28. Loading States

Every processing action must provide a visible state such as:
- Initializing camera
- Loading YOLO
- Detecting objects
- Reading text
- Understanding scene
- Listening
- Generating response
- Speaking

## 29. Empty States

Examples:
- No camera frame captured.
- No objects detected.
- No readable text detected.
- No voice input detected.
- No AI response available.

## 30. Error States

Handle:
- Camera unavailable
- Microphone unavailable
- Model loading failure
- YOLO inference failure
- OCR failure
- AI API timeout
- AI API quota/authentication failure
- STT failure
- TTS failure
- Invalid configuration
- Network failure

Use safe user-facing messages.

## 31. Success States

Examples:
- Camera connected
- YOLO ready
- OCR complete
- Scene description generated
- Text extracted
- Voice response generated
- Safety Mode active

## 32. Custom 404 / Invalid Route

If Streamlit routing or deployment exposes unsupported paths, provide a friendly fallback/error state rather than internal exceptions.

## 33. Thank-You Page

Not required for the core prototype. If feedback/contact is added later, implement a real submission workflow before adding a thank-you screen.

## 34. Privacy Policy

If deployed publicly, document:
- Camera access
- Microphone access
- Image/audio transmission
- AI provider processing
- Retention
- Third-party services
- User controls
- Contact information

Unknown policy details are **To Be Decided**.

## 35. Terms & Conditions

Include:
- Prototype nature
- No guaranteed collision avoidance
- No medical claims
- Appropriate-use limitations
- Third-party service dependencies
- User responsibility

## 36. Cookie Requirements

No cookies are required for the local prototype. If analytics, authentication, or deployment infrastructure introduces cookies, provide appropriate disclosure/consent where legally applicable.

## 37. Analytics

Analytics are optional and should not collect sensitive camera/audio content by default. Any analytics provider and retention policy are **To Be Decided**.

## 38. Image Optimization

- Resize before expensive inference where appropriate.
- Use suitable JPEG/WebP representations when supported.
- Avoid storing images unless explicitly required.
- Do not retain camera frames by default.
- Avoid uploading continuous video to external AI APIs.

## 39. Metadata

Configure title, description, favicon, and Open Graph metadata for public deployments.

## 40. Sitemap

Only create a sitemap for indexable public routes. The interactive app itself does not require a complex sitemap.

## 41. robots.txt

Define indexing policy explicitly. For a private/demo deployment, disallow indexing. For a public product landing page, allow only intended public routes.

## 42. Open Graph

Use a professional VisionMate AI product image with accurate title/description. The final asset is **To Be Decided**.

## 43. Complete End-to-End Flow

Camera → frame capture → image preprocessing → selected AI pipeline → result → UI display → optional TTS → speaker/earphone.

Voice flow:
Microphone → speech-to-text → question + image → vision AI → response → text-to-speech → audio output.

## 44. Acceptance Criteria

The prototype is acceptable when:
1. Camera input works.
2. YOLO detection works on a test image/frame.
3. Scene description works with a configured vision model.
4. OCR extracts readable text.
5. TTS speaks OCR/AI responses.
6. Voice questions can be processed.
7. Safety Mode produces clearly labeled prototype warnings.
8. System status accurately reflects readiness/errors.
9. API keys are not present in source code.
10. Application handles provider/network failures safely.
11. Desktop and supported mobile/tablet layouts are usable.
12. No critical console/runtime errors remain.
13. The camera abstraction is documented for future smart-spectacles integration.

## 45. Success Metrics

Technical prototype metrics:
- Successful camera initialization rate during testing.
- Object detection response time.
- OCR response time.
- Scene-response latency.
- Voice pipeline latency.
- Number of critical runtime errors.
- Successful completion rate for defined demo flows.

Exact target thresholds are **To Be Decided** after hardware/model selection.

## 46. Definition of Done

A feature is done only when it is implemented, run, tested, errors fixed, re-tested, and verified against existing features.

Required workflow:

**INSPECT → IMPLEMENT → RUN → TEST → IDENTIFY ERROR → FIX → RE-RUN → RE-TEST → REGRESSION CHECK → CONTINUE**

## 47. Final Product Checklist

- [ ] Camera works
- [ ] Capture works
- [ ] YOLO works
- [ ] Bounding boxes render
- [ ] Scene description works
- [ ] OCR works
- [ ] TTS works
- [ ] STT works
- [ ] Voice assistant works
- [ ] Safety Mode works as an assistive prototype
- [ ] Status indicators are accurate
- [ ] Errors are handled safely
- [ ] API keys are secured
- [ ] UI is responsive
- [ ] Accessibility checks completed
- [ ] Performance checks completed
- [ ] Production build/deployment tested
- [ ] Privacy/terms requirements reviewed
- [ ] Smart-spectacles integration points documented
