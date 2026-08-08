# Sinovox Designer — Design QA

## Target and implementation

- Reference: user-supplied Sinovox Chinese console screenshot, 1024 × 792.
- Implementation: `index.html`, checked at 1024 × 792 in the default Rice paper skin.
- Core flow: page loads → Live Voice screen renders → voice selection changes → Pinyin helper expands.

## Visual comparison

The supplied reference and the 1024 × 792 implementation capture were compared together for hierarchy, scale, alignment, typography, palette, asset treatment, and first-viewport content.

| Reference evidence | Rendered evidence | Resolution |
| --- | --- | --- |
| Black lacquer header with gold brand and compact device status | Same compact dark header, gold bilingual brand, transport labels, and live connection status | Matched |
| Serial and MIDI controls share one shallow strip | Both connection groups sit in one compact two-column strip | Matched |
| Text-to-speech is the first and largest live control | Large rice-paper text box appears first with vertical Speak/Clear controls | Matched |
| Language, six illustrated voices, and three brass controls share one row | Six generated ink portraits and three generated brass knobs form the same compact control row | Matched |
| Serial monitor remains visible in the initial 1024 × 792 viewport | Monitor heading and full terminal area are visible without scrolling | Matched |
| Reference has no always-open translation workflow | Existing English-to-Pinyin workflow is preserved behind a compact expandable disclosure | Intentional functional extension |
| Reference depicts a connected device | Header status now reflects actual serial/MIDI state instead of always claiming connection | Intentional accuracy improvement |

## Functional checks

- Page identity and meaningful content: passed.
- Blank/error-overlay check: passed.
- Generated portrait, knob, and paper assets load: passed.
- Voice interaction: programmatic user click selected Voice 3 and updated the active card: passed.
- Pinyin disclosure: opened and preserved the existing English, Chinese, and numbered-Pinyin fields: passed.
- Pinyin Converter is restored as a visible top-level tab: passed.
- Select/Disconnect/Identify/Refresh controls for Serial and Connect/Identify/Refresh controls for MIDI are visible; their original handlers remain wired: passed.
- Responsive narrow-layout overflow corrections added for connection controls and voice cards.
- Hardware-only Serial and MIDI connection behavior was not exercised in the headless browser; existing handlers were preserved.

## Browser note

The in-app Browser was listed but returned `No browser is available`. Following the established local fallback, validation used local headless Chrome. Chrome updater/GCM messages were external browser-process noise; the page rendered and the interaction probe reported `Sinovox QA Interaction Passed` and `data-qa-interaction="passed"`.

## Result

final result: passed
