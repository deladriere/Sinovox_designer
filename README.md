# Sinovox 声音工坊

Browser control surface for Kraftor Sinovox firmware. GUI v1.2 provides live
Chinese/Pinyin or English speech over USB Serial, complete MIDI voice control,
RAM/FRAM sentence editing and printable MIDI reference sheets.

## Features

- Speak ASCII Pinyin or English over USB Serial at 115200 baud.
- Translate English to Simplified Chinese with Chrome's local Translator API,
  then create compact numbered Sinovox Pinyin in the browser.
- Read board model, chip ID, firmware version and storage layout from `!INFO?`.
- Select all six Sinovox speakers.
- Control language, pitch, speed and volume over serial and MIDI.
- Match MIDI channels 1–15 to the Kraftor DIP switches.
- Edit 20 RAM sentences and up to 100 persistent FRAM sentences.
- Bulk-fill sentence banks and print note-reference sheets.
- Five visual skins based on rice paper, lacquer, jade, peony and midnight.

## Requirements

- Chrome or Edge with Web Serial and Web MIDI.
- Kraftor running `Kraftor_SInovox_Serial&MIDI` firmware v1.0 or later.
- Sinovox connected to Kraftor `Serial5`.

Open `index.html`, click **Select port**, then choose the Kraftor USB serial
device. The GUI sends `!INFO?` and displays the detected model and firmware.

## Voice controls

The GUI keeps USB Serial and MIDI controls aligned with the firmware:

| Control | Range | MIDI |
| --- | --- | --- |
| Voice | indices 0–5, speakers 3/51/52/53/54/55 | CC 1 |
| Pitch | 0–10 | Pitch bend |
| Speed | 0–10 | CC 2 |
| Volume | 0–10 | CC 3 |
| Language | 0 English, 1 Chinese/Pinyin | CC 4 |

Over serial the same state is sent as:

```text
!VOICE language pitch speed voice volume
```

The firmware creates the Sinovox tags in the correct order:
`[i][h2][t][s][m][v]`. Store and send only the text to speak.

## English to Sinovox Pinyin

Enter English in the translation helper and click **Translate**. On supported
desktop Chrome versions, the browser translates locally to Simplified Chinese;
the bundled browser converter then produces numbered Pinyin. If local
translation is unavailable, **Google fallback** opens a prefilled translation:
paste its Simplified Chinese result into step 2 and convert it locally.

The helper lowercases the output, removes spaces and punctuation, converts
`ü` to ASCII `v`, and selects Chinese/Pinyin mode when the result is placed in
the speech box. It does not add `[i1]`; the firmware adds that tag.

## Sentence banks

| MIDI notes | Result |
| --- | --- |
| 28–47 | Play RAM slots 0–19 |
| 48–127 | Play FRAM slots 0–79 |

FRAM slots 80–99 remain available through the serial interface. Sentence
length is limited to 200 ASCII bytes.

See [user_manual.html](user_manual.html) for the full workflow and commands.
