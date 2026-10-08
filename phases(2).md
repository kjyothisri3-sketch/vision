# phases.md — VisionMate AI

## Development Rule

The project must be developed continuously with verification after every major feature.

**Required workflow:**

```text
INSPECT
→ IMPLEMENT
→ RUN
→ TEST
→ IDENTIFY ERROR
→ FIX
→ RE-RUN
→ RE-TEST
→ VERIFY EXISTING FEATURES
→ CONTINUE
```

Do not accumulate known errors.

---

# PHASE 1 — Project Planning & Setup

## Objective

Establish the VisionMate AI development environment and modular project foundation.

## Tasks

### 1.1 Requirements Finalization
- Confirm live camera requirement.
- Confirm YOLO requirement.
- Confirm OCR requirement.
- Confirm vision AI requirement.
- Confirm STT/TTS requirements.
- Confirm Safety Mode limitation.
- Confirm laptop/browser camera as prototype source.
- Document future smart-spectacles integration.

### 1.2 Project Initialization
- Create Python project.
- Create virtual environment.
- Add `app.py`.
- Create modular directories.
- Create `requirements.txt`.
- Create `.gitignore`.
- Create `.env.example`.

### 1.3 Git/GitHub
- Initialize Git.
- Create repository.
- Commit project skeleton.
- Ensure `.env` is ignored.

### 1.4 Environment
Configure:
- Python version
- OCR dependency
- YOLO dependency
- OpenCV
- Streamlit
- STT/TTS libraries
- Selected vision AI SDK/API client

## Dependencies

None.

## Expected Output

Runnable empty Streamlit shell with configuration loading.

## Testing Checkpoint

- Virtual environment activates.
- `streamlit run app.py` starts.
- Configuration loads without exposing secrets.
- Git repository is clean of credentials.

## Completion Criteria

The project launches successfully and has a modular structure.

---

# PHASE 2 — Design & UI System

## Objective

Build the futuristic accessibility-focused interface before connecting all AI services.

## Tasks

### 2.1 Brand
- Add VisionMate AI header.
- Add tagline: “See • Understand • Stay Safe”.
- Add favicon where supported.

### 2.2 Visual System
- Dark navy/black background.
- Blue/purple accents.
- High-contrast text.
- Rounded cards.
- Readable typography.

### 2.3 Core Components
Build:
- Header
- Camera panel
- Feature action bar
- Results panel
- Safety alert
- Voice output indicator
- System status
- Footer
- Prototype disclaimer

### 2.4 Responsive System
Test:
- Desktop
- Laptop
- Tablet
- Mobile browser where supported

## Dependencies

Phase 1.

## Expected Output

Professional static UI shell with no fake functional results.

## Testing Checkpoint

- UI renders.
- Buttons have correct states.
- No horizontal overflow.
- Text remains readable.
- Focus/keyboard behavior is checked where supported.

## Completion Criteria

The visual shell is approved and ready for integration.

---

# PHASE 3 — Public/Application Interface Development

## Objective

Implement the main VisionMate interaction experience.

## Tasks

### 3.1 Camera
- Connect laptop/browser camera.
- Display live feed.
- Add capture control.
- Handle permission denial.
- Show connected/unavailable state.

### 3.2 Feature Controls
Implement:
- Describe Scene
- Detect Objects
- Read Text
- Safety Mode
- Ask VisionMate

### 3.3 Results
Create separate result sections for:
- Objects
- OCR text
- AI response
- Safety alerts

### 3.4 Voice Indicator
Display listening/speaking states.

## Dependencies

Phase 2.

## Expected Output

Camera-first application with real controls and real input state.

## Testing Checkpoint

- Camera opens.
- Capture works.
- Camera failure is handled.
- Feature buttons do not pretend to work before their backend is connected.

## Completion Criteria

The main UI can capture and pass a frame to the processing layer.

---

# PHASE 4 — Backend, AI Pipeline & Processing

## Objective

Connect the real computer-vision and AI services.

## Tasks

### 4.1 OpenCV
- Frame conversion.
- Resize/preprocessing.
- Image encoding.
- Performance measurement.

### 4.2 YOLO
- Install/load model.
- Cache model instance.
- Run inference.
- Filter confidence.
- Draw bounding boxes.
- Display labels and confidence.

### 4.3 OCR
- Integrate Tesseract or EasyOCR.
- Preprocess image.
- Extract text.
- Handle empty output.
- Send extracted text to TTS.

### 4.4 Vision AI
- Select provider.
- Configure API key through environment variables.
- Encode image.
- Add scene-description prompt.
- Add image-question prompt.
- Set timeout/error handling.
- Display concise response.

### 4.5 Orchestration
Create a common service layer so UI code does not contain provider-specific implementation.

## Dependencies

Phase 3.

## Expected Output

Real object detection, OCR, and scene understanding.

## Testing Checkpoint

For each feature:

1. Inspect.
2. Implement.
3. Run.
4. Test.
5. Identify errors.
6. Fix.
7. Re-run.
8. Re-test.
9. Regression test.

## Completion Criteria

No core AI feature uses fake responses.

---

# PHASE 5 — Voice Assistant & Safety Mode

## Objective

Complete voice interaction and experimental safety warnings.

## Tasks

### 5.1 Speech-to-Text
- Capture microphone input.
- Transcribe speech.
- Display recognized question.
- Handle permission and recognition errors.

### 5.2 Ask VisionMate
Flow:

```text
User speech
→ STT
→ Current image
→ User question + image
→ Vision AI
→ Response
```

### 5.3 Text-to-Speech
- Speak AI responses.
- Speak OCR text.
- Speak safety warnings.
- Display speaking state.

### 5.4 Safety Mode
- Continuous/periodic frame analysis.
- Object detection.
- Relevant object filtering.
- Warning thresholds.
- Warning cooldown.
- Visual alert.
- Audio alert.

### 5.5 Safety Disclaimer
Clearly show:

**“Safety Mode is an assistive prototype and does not guarantee collision avoidance.”**

## Dependencies

Phase 4.

## Expected Output

End-to-end voice and safety workflows.

## Testing Checkpoint

- STT success/failure.
- AI question response.
- TTS output.
- Safety warning cooldown.
- No repeated audio flooding.
- Safety limitation is always visible where appropriate.

## Completion Criteria

Voice assistant and Safety Mode operate with real implementations.

---

# PHASE 6 — Content, Configuration & Media

## Objective

Make the application maintainable and ready for demonstration/deployment.

## Tasks

### 6.1 Configuration
- Centralize settings.
- Use `.env`.
- Provide `.env.example`.
- Validate configuration at startup.

### 6.2 Image Handling
- Resize frames where appropriate.
- Avoid unnecessary storage.
- Avoid unnecessary external uploads.

### 6.3 Status System
System status must reflect real runtime readiness:
- Camera
- YOLO
- OCR
- AI
- Voice

### 6.4 Error Messaging
Add safe user-facing messages for every provider/device failure.

## Dependencies

Phases 4–5.

## Expected Output

Stable configurable application.

## Testing Checkpoint

Restart application with:
- Missing API key.
- Missing model.
- Camera unavailable.
- OCR unavailable.
- Microphone unavailable.
- Network unavailable.

Verify graceful behavior.

## Completion Criteria

Configuration and failure handling are production-quality for the prototype.

---

# PHASE 7 — SEO & Performance

## Objective

Optimize the application and public-facing metadata where applicable.

## Tasks

### 7.1 Metadata
- VisionMate AI title.
- Accurate description.
- Favicon.
- Open Graph asset where deployment supports it.

### 7.2 Indexing
- Decide whether demo should be indexed.
- Configure `robots.txt` accordingly.
- Add sitemap only for intended public pages.

### 7.3 Performance
- Cache YOLO model.
- Resize frames.
- Reduce unnecessary inference frequency.
- Add AI request cooldown.
- Add TTS cooldown.
- Measure latency.
- Avoid processing full-resolution frames unnecessarily.

### 7.4 Resource Testing
Measure:
- CPU
- RAM
- GPU if available
- Model loading time
- Detection latency
- OCR latency
- AI latency
- Voice latency

## Dependencies

Phases 4–6.

## Expected Output

Faster and more predictable demo experience.

## Testing Checkpoint

Compare baseline and optimized processing time.

## Completion Criteria

No obvious performance bottlenecks remain for the selected hardware.

---

# PHASE 8 — Security & Testing

## Objective

Verify the complete application before deployment.

## Tasks

### 8.1 Code Quality
- Run Python linting.
- Check imports.
- Remove dead code.
- Run type/static checks where configured.

### 8.2 Runtime
- Start Streamlit.
- Check console logs.
- Check browser behavior.
- Check for uncaught exceptions.

### 8.3 AI Pipeline Testing
- YOLO detection.
- OCR.
- Vision AI.
- STT.
- TTS.
- Safety.

### 8.4 Input Testing
Test:
- Empty input
- Invalid configuration
- Large images
- Unsupported image data
- Empty OCR
- No detected objects
- No voice
- Long AI response

### 8.5 Security Testing
Verify:
- No secrets in source.
- `.env` ignored.
- API keys not displayed.
- Errors do not reveal stack traces to users.
- No unsafe HTML rendering.
- Provider credentials use least privilege.
- HTTPS is used in production.
- External requests have timeouts.
- Rate/cooldown controls exist.

### 8.6 Responsive Testing
Verify:
- Desktop
- Laptop
- Tablet
- Mobile where supported

### 8.7 Accessibility
Verify:
- Contrast
- Readability
- Button size
- Keyboard interaction where supported
- Text equivalent of voice results
- Warning visibility

### 8.8 End-to-End Testing
Run:

```text
Open app
→ Connect camera
→ Capture
→ Detect objects
→ Describe scene
→ Read text
→ Ask question
→ Receive spoken response
→ Enable Safety Mode
→ Trigger test warning
→ Disable Safety Mode
```

## Dependencies

Phases 1–7.

## Expected Output

Verified release candidate.

## Testing Checkpoint

All tests must actually be executed, not merely documented.

## Completion Criteria

No known critical or high-severity defect remains.

---

# PHASE 9 — Deployment

## Objective

Deploy the application using infrastructure compatible with Python, Streamlit, camera access, and selected AI models.

## Tasks

### 9.1 Production Environment
- Create production environment.
- Configure secrets.
- Disable debug behavior.
- Configure resource limits.

### 9.2 Deployment Platform
Choose a Streamlit/Python-capable deployment platform based on camera and model requirements.

Vercel is not required for the Streamlit runtime.

### 9.3 HTTPS
- Enable HTTPS.
- Verify secure external API calls.

### 9.4 Domain
Domain is **To Be Decided**.

### 9.5 Production Verification
- Camera.
- Microphone.
- YOLO.
- OCR.
- AI.
- STT.
- TTS.
- Safety Mode.

### 9.6 SEO/Security
- Final metadata.
- Robots policy.
- Security configuration.
- Privacy/terms availability.

## Dependencies

Phase 8.

## Expected Output

Production/demo deployment.

## Testing Checkpoint

Run the complete end-to-end flow against the deployed environment.

## Completion Criteria

Deployment works without critical runtime/configuration errors.

---

# PHASE 10 — Launch & Post-Launch

## Objective

Perform final verification and establish maintenance practices.

## Tasks

### 10.1 Final QA
- Verify every feature.
- Verify all system statuses.
- Verify error states.
- Verify responsive UI.

### 10.2 Content Verification
- Product name.
- Tagline.
- Safety disclaimer.
- Privacy policy.
- Terms.

### 10.3 Analytics
If analytics are implemented:
- Verify events.
- Verify no sensitive camera/audio data is collected.
- Verify consent requirements where applicable.

### 10.4 Backup
- Verify Git repository.
- Verify `.env.example`.
- Document model setup.
- Document deployment configuration.

### 10.5 Monitoring
Monitor:
- Runtime errors.
- AI provider failures.
- Model failures.
- Resource usage.
- User-reported problems.

### 10.6 Smart-Spectacles Readiness
Confirm that the camera abstraction is documented and the future integration boundary is clear.

## Dependencies

Phase 9.

## Expected Output

Launch-ready VisionMate AI prototype with maintenance documentation.

## Testing Checkpoint

Run complete launch checklist.

## Completion Criteria

All release criteria pass.

---

# Continuous Feature Development Checklist

For every major feature:

### Step A — Inspect
Understand existing implementation before editing.

### Step B — Implement
Implement the smallest complete version.

### Step C — Test Immediately
Run the application and test the feature.

### Step D — Fix
Identify root cause, fix it, re-run, and re-test.

### Step E — Regression Check
Verify existing features still work.

### Step F — Continue
Move to the next feature only after the checkpoint passes.

---

# Supabase Verification Note

Supabase is **not required for the current VisionMate AI prototype** because the specified core functionality does not require persistent application data.

If future requirements add Supabase:

1. Create schema.
2. Apply migrations.
3. Verify tables.
4. Verify columns.
5. Verify relationships.
6. Enable and verify RLS.
7. Verify policies.
8. Verify connection.
9. Test INSERT.
10. Test SELECT.
11. Test UPDATE.
12. Test DELETE where applicable.
13. Test authorization.

Never substitute:
- Local JSON
- In-memory records
- Hardcoded records
- Fake APIs

for real persistence when persistence becomes a requirement.

---

# Final Launch Checklist

- [ ] Requirements verified
- [ ] Python environment verified
- [ ] Streamlit starts
- [ ] Camera works
- [ ] Capture works
- [ ] YOLO works
- [ ] OCR works
- [ ] Vision AI works
- [ ] STT works
- [ ] TTS works
- [ ] Safety Mode works
- [ ] Safety disclaimer visible
- [ ] Real system status implemented
- [ ] No fake functionality
- [ ] No secrets committed
- [ ] Error handling verified
- [ ] Responsive testing completed
- [ ] Accessibility testing completed
- [ ] Performance testing completed
- [ ] Security testing completed
- [ ] Production deployment tested
- [ ] Privacy/Terms reviewed
- [ ] Git backup verified
- [ ] Future smart-spectacles integration documented
