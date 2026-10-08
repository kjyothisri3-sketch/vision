# design.md — VisionMate AI

## 1. Design Philosophy

VisionMate AI should feel like a real accessibility-focused AI product rather than a tutorial. The interface should prioritize:

1. Clarity
2. High contrast
3. Large interaction targets
4. Minimal cognitive load
5. Voice-first feedback
6. Immediate system status
7. Clear separation between visual results and actions
8. Safe communication of prototype limitations

## 2. Brand Direction

**Product:** VisionMate AI

**Tagline:** “See • Understand • Stay Safe”

The brand should communicate intelligent vision assistance, trust, accessibility, and modern AI.

## 3. Visual Style

- Futuristic but practical
- Dark navy/black foundation
- Blue and purple accents
- High-contrast text
- Rounded cards
- Clean iconography
- Subtle gradients/glows
- Controlled motion
- No excessive decoration

## 4. Color System

The supplied direction is the primary reference:

| Token | Suggested Value | Usage |
|---|---|---|
| Background | `#070B18` | Main background |
| Surface | `#10172A` | Cards/panels |
| Elevated Surface | `#151D33` | Interactive panels |
| Primary Blue | `#3B82F6` | Main CTA |
| Accent Purple | `#8B5CF6` | AI/voice accents |
| Text Primary | `#F8FAFC` | Main text |
| Text Secondary | `#CBD5E1` | Supporting text |
| Success | `#22C55E` | Ready/success |
| Warning | `#F59E0B` | Caution |
| Error | `#EF4444` | Errors |
| Border | `#26324D` | Card/input borders |

These are implementation defaults derived from the requested dark navy/black + blue/purple direction and may be refined during implementation.

## 5. Typography

Use a modern sans-serif system font stack for the prototype unless a final brand font is selected.

Recommended hierarchy:
- Display: 32–48px
- H1: 28–36px
- H2: 22–28px
- H3: 18–22px
- Body: 16px
- Supporting: 14px
- Caption: 12–13px

## 6. Font Weights

- Regular: 400
- Medium: 500
- Semibold: 600
- Bold: 700

Avoid excessive use of bold text.

## 7. Spacing System

Use a consistent 4px/8px-oriented scale:
- 4px
- 8px
- 12px
- 16px
- 24px
- 32px
- 48px
- 64px

## 8. Border Radius

- Small controls: 8px
- Inputs/buttons: 10–12px
- Cards: 16px
- Hero/camera container: 20px
- Pills/status tags: 999px

## 9. Shadows

Use restrained shadows/glows:
- Card: subtle dark shadow
- Active AI panel: subtle blue/purple glow
- Warning: controlled warning glow
- Avoid heavy neon effects that reduce readability

## 10. Buttons

### Primary
Used for major actions such as Describe Scene.

### Secondary
Used for Detect Objects, Read Text, and other supporting actions.

### Danger/Warning
Safety Mode should use strong warning semantics without relying only on color.

Buttons must:
- Have clear labels
- Be large enough for touch
- Show disabled/loading states
- Avoid icon-only critical actions

## 11. Cards

Use cards for:
- Camera panel
- Results
- Detected objects
- OCR output
- AI response
- Safety alert
- System status

Cards should have consistent padding, radius, border, and hierarchy.

## 12. Forms

Keep forms minimal. Configuration controls should not distract from the main camera experience.

## 13. Inputs

Inputs require:
- Visible labels
- Helpful placeholders only when needed
- Clear validation
- Error text
- Keyboard accessibility
- Sufficient contrast

## 14. Dropdowns

Use dropdowns for:
- OCR provider
- Optional camera source
- Optional model/provider selection

Do not place API secrets in inputs.

## 15. Navigation

The application should use simple navigation or grouped controls. The five core capabilities should always be discoverable.

## 16. Header

Header content:

**👁️ VisionMate AI**

Subtitle:
**See • Understand • Stay Safe**

Include a compact system/readiness indicator where space permits.

## 17. Footer

Footer should contain:
- VisionMate AI
- Prototype disclaimer
- Privacy link if deployed publicly
- Terms link if deployed publicly
- Version/build indicator if useful

## 18. Hero Section

The hero should quickly communicate:
- What VisionMate AI does
- Camera-first interaction
- Voice feedback
- Prototype limitation

Primary action should lead the user to the camera workspace.

## 19. CTA Sections

Primary actions:
- Describe Scene
- Detect Objects
- Read Text
- Safety Mode
- Ask VisionMate

The most frequently used action should remain visually prominent.

## 20. Page Layouts

### Desktop

Two major zones:
1. Camera/workspace
2. Results/status

Suggested layout:

```text
┌──────────────────────────────────────────────────────┐
│ VisionMate AI                 System Status           │
├───────────────────────────┬──────────────────────────┤
│                           │ Results                  │
│      LIVE CAMERA          │ Detected Objects         │
│                           │ OCR Text                │
│      Capture              │ AI Response             │
│                           │ Safety Alert            │
├───────────────────────────┴──────────────────────────┤
│ Describe | Detect | Read | Safety | Ask VisionMate   │
└──────────────────────────────────────────────────────┘
```

## 21. Section Layouts

Results should be ordered by relevance:
1. Active result
2. Safety alert
3. Object detections
4. OCR
5. AI response
6. System status

## 22. Mobile Layout

Stack sections vertically:

```text
Header
Camera
Capture
Feature buttons
Active result
Safety alert
Objects
OCR
AI response
System status
Footer
```

Use large touch targets and avoid dense tables.

## 23. Tablet Layout

Use a flexible two-column layout where screen width permits. Collapse to one column when content becomes cramped.

## 24. Desktop Layout

Use a wider camera panel with a fixed-width or flexible results panel. Preserve enough space for bounding-box visualization.

## 25. Responsive Breakpoints

Suggested:
- Mobile: < 640px
- Tablet: 640–1023px
- Desktop: ≥ 1024px
- Wide desktop: ≥ 1440px

These are UI design breakpoints; actual Streamlit behavior must be tested in the target deployment.

## 26. Components

Core components:
- `AppHeader`
- `CameraPanel`
- `CaptureControl`
- `FeatureActionBar`
- `ObjectDetectionPanel`
- `OCRPanel`
- `SceneDescriptionPanel`
- `SafetyAlert`
- `VoiceAssistantPanel`
- `VoiceOutputIndicator`
- `SystemStatus`
- `ProcessingIndicator`
- `ErrorMessage`
- `PrototypeDisclaimer`
- `Footer`

## 27. Component States

Every interactive component should support:
- Default
- Hover where supported
- Focus
- Active
- Disabled
- Loading
- Success
- Error
- Empty

## 28. Hover States

Hover should slightly elevate or brighten controls without changing layout.

## 29. Focus States

Keyboard focus must be clearly visible. Do not remove browser/application focus indication without replacing it.

## 30. Active States

Selected feature actions should clearly indicate the current operation.

## 31. Disabled States

Disabled buttons should communicate why they are unavailable where practical, e.g. no captured frame or required service unavailable.

## 32. Loading States

Use:
- Spinner/progress indicator
- Short status text
- Disabled duplicate action
- Optional elapsed/processing indicator for long requests

## 33. Empty States

Use clear messages:
- “Capture an image to begin.”
- “No readable text detected.”
- “No objects detected.”
- “Ask a question after capturing a scene.”

## 34. Error States

Use concise, non-technical messages:
- “Camera access is unavailable.”
- “Object detection could not be completed.”
- “The AI service is temporarily unavailable.”

Developer details should be logged separately.

## 35. Animations

Use subtle transitions:
- Card appearance
- Result updates
- Status changes
- Voice activity
- Detection result emphasis

Do not animate continuously in a way that distracts or harms accessibility.

## 36. Page Transitions

Streamlit navigation should prioritize fast state changes rather than elaborate transitions.

## 37. Image Guidelines

- Camera frames should preserve useful visual detail.
- Resize for inference when possible.
- Do not store images by default.
- Avoid unnecessary external uploads.
- Use optimized formats for stored product assets.

## 38. Icon Guidelines

Use simple recognizable icons:
- Eye
- Target
- Book/text
- Warning
- Microphone
- Volume
- Camera
- Check/status

Icons should supplement labels, not replace critical labels.

## 39. Accessibility

- High contrast
- Large text
- Large controls
- Clear labels
- No color-only meaning
- Text equivalents for spoken results
- Captions/transcripts where applicable
- Keyboard navigation where supported
- Reduced-motion consideration
- Clear error text

## 40. Visual Hierarchy

Priority:
1. Camera
2. Feature controls
3. Current result
4. Safety status
5. Supporting results
6. System diagnostics

## 41. Content Hierarchy

Keep AI-generated output concise. Prefer:
- Short sentence
- Bullet list
- Clearly labeled detection list
- Readable OCR block

Avoid dumping raw model output into the interface.

## 42. CTA Placement

The five feature buttons should be immediately below or beside the camera workspace. Capture should be close to the camera.

## 43. Form UX

Configuration should be visually separated from normal usage. Defaults should allow the demo to run without unnecessary configuration.

## 44. Admin Dashboard UI

No admin dashboard is required in the current scope.

If introduced later, it must use real data and real actions rather than mock statistics or placeholder CRUD.

## 45. Admin Tables

Not applicable to current scope.

## 46. Admin Forms

Not applicable to current scope.

## 47. Admin Navigation

Not applicable to current scope.

## 48. Safety UX

Safety Mode should always display:
- ACTIVE/INACTIVE state
- Current warning state
- Prototype disclaimer
- Last warning
- Audio warning state

Never present a green “safe” state as a guarantee that the environment is free of obstacles.

## 49. Voice UX

When listening:
- Show microphone/listening indicator.
- Display recognized speech when available.

When speaking:
- Show “Speaking”.
- Provide text equivalent.

When voice fails:
- Give a visual error and allow text interaction where available.

## 50. System Status

Display:
- Camera: Connected/Unavailable
- YOLO: Ready/Error
- OCR: Ready/Error
- AI: Ready/Error
- Voice: Ready/Error

Status should reflect actual runtime state and must not be hardcoded.

## 51. Design Quality Gate

Before completion verify:
- All five feature controls are visually distinct.
- Camera is the visual focal point.
- Results are readable.
- Warning states are obvious.
- Mobile layout remains usable.
- Text contrast is sufficient.
- No fake status is displayed.
