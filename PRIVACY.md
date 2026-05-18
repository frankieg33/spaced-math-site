# Privacy Policy — Spaced Math

**Effective date:** 2026-05-17
**Last updated:** 2026-05-17

This policy describes how the Spaced Math iOS app ("the App") handles your information. It applies to v1.0 onward.

## Summary in plain English

- We don't run any servers. We don't collect any personal information.
- Everything stays on your device unless you turn on **iCloud sync**, in which case Apple — not us — stores it in your private iCloud account.
- The App uses your microphone only while you're answering a problem in voice mode. Audio is processed by Apple's on-device / Siri-class speech recognition and immediately discarded; we never store, upload, or analyze it.
- There are no third-party trackers, no ads, and no analytics SDKs.

## What the App stores on your device

- **Profiles.** Name, emoji, color, and per-profile settings.
- **Spaced-repetition state.** For each card (e.g. `7 + 8`): scheduled next-review date, difficulty, stability, and review count.
- **Activity.** A per-day count of completed reviews per profile (used for the streak chip and the Stats screen).
- **Mistakes.** A queue of problems you've recently answered incorrectly so the App can re-surface them.
- **Preferences.** App-wide toggles like whether iCloud sync is enabled.

All of this is written to the App's own sandboxed Documents folder and to `UserDefaults`. The App can't read other apps' data, and other apps can't read the App's data.

## What the App optionally stores in iCloud

iCloud sync is **off by default**. When you turn it on (Settings → iCloud → Use iCloud), the App writes the same data described above to your private iCloud key-value store using Apple's `NSUbiquitousKeyValueStore` API. This is your iCloud, accessible only to you on devices signed in to the same Apple ID. We have no access to it.

- The exact data synced: profiles, card states, activity, mistakes, and the slot index.
- iCloud sync **does not** include the contents of any voice recording or any analytics.
- When you sign into a different Apple ID, the App detects the change and turns sync off until you explicitly turn it back on, so data isn't silently uploaded to a different account.
- Deleting a profile from **Manage Profiles** removes the profile from the device and (when iCloud is reachable on the originating Apple ID) from your iCloud copy as well.

## Microphone & speech recognition

When voice mode is enabled, while you're answering a problem the App:

1. Captures live microphone audio with `AVAudioEngine`.
2. Streams it to `SFSpeechRecognizer` (Apple's framework). On modern iOS devices recognition runs on-device by default; some configurations may use Apple's speech-recognition servers.
3. Reads the transcribed digits and grades the answer.
4. Stops capture as soon as a final answer is obtained.

We do not retain audio, transcripts, or any derived signal. We do not transmit audio to any party other than Apple's `SFSpeechRecognizer`. The App requests `NSMicrophoneUsageDescription` and `NSSpeechRecognitionUsageDescription` at first use; if either permission is denied, voice mode is automatically disabled and the on-screen number pad is used instead.

## Diagnostic logs

The App emits unstructured diagnostic events through Apple's standard `OSLog` framework (e.g. "study session ended, correct=12 wrong=3"). These logs:

- Stay on the device.
- Are visible only to you, in Console.app while the device is connected to a Mac.
- Use Apple's `.private` privacy classification for any potentially user-identifying value (profile id, profile name), so those values are redacted in shipped builds.

We do not collect, retrieve, or transmit `OSLog` content.

## Data we do NOT collect

- Your name, email, or contact info.
- Your location.
- Any device identifier (IDFA, IDFV, advertising id).
- Crash reports beyond what Apple may collect through your iOS settings.
- Any analytics or behavioral telemetry.

## Children's privacy

Spaced Math is designed to be safe for children. Because the App collects no personal information and contacts no third parties, it complies with COPPA's "no personal information" definition. We don't display ads, and there are no in-app purchases, accounts, or social features.

## Your choices

- **Disable voice mode** at any time per profile (Settings → Voice mode), or globally by denying microphone permission in iOS Settings.
- **Disable iCloud sync** at any time (Settings → iCloud → Use iCloud → off). Disabling does not delete iCloud copies; delete each profile individually if you want them removed.
- **Reset a profile's progress** without deleting the profile (Settings → Reset this profile's progress).
- **Delete a profile** (Manage Profiles → swipe or tap to delete) — also removes the iCloud copy when sync is on. Repeat per profile to remove everything.

## Changes to this policy

If we change this policy, the new version will be available at the same URL with an updated **Last updated** date. Material changes will also be noted in the App's release notes.

## Contact

Questions about this policy or your data? Email **spacedmath@gmail.com**.