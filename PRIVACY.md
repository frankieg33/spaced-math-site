# Privacy Policy — Spaced Math

**Effective date:** 2026-05-21
**Last updated:** 2026-06-10

This policy describes how the Spaced Math iOS app ("the App") handles your information. It applies to v1.0 onward, including the v3 single-household CloudKit sharing model (which replaces v2.0's per-profile sharing).

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

iCloud sync is **off by default**. When you turn it on (gear icon → **Settings → Sync → Use iCloud**), the App writes the same data described above to your private iCloud using Apple's **CloudKit** API. This is your iCloud, accessible only to you on devices signed in to the same Apple ID. We have no access to it.

- The exact data synced: profiles, card states, activity, mistakes, and (optionally) household share metadata (a display name you choose for your household).
- iCloud sync **does not** include the contents of any voice recording or any analytics.
- When you sign into a different Apple ID, the App detects the change and turns sync off until you explicitly turn it back on, so data isn't silently uploaded to a different account.
- Deleting a profile from **Manage Profiles** removes the profile from the device and (when iCloud is reachable on the originating Apple ID) from your iCloud copy as well.

## Household sharing

In v3, sharing happens at the **household** level rather than per profile. Open the gear icon → **Settings → Household → Set up household**, name your household, and invite family members through the standard iOS share sheet (Messages, Mail, or AirDrop).

- All profiles on the owner's device belong to the household. Inviting a family member shares them all at once.
- Data lives in the **household owner's iCloud**. Participants don't store a separate copy in their own iCloud; their study activity writes directly to the owner's CloudKit through Apple's zone-scoped CKShare permission model.
- Joining a household is **destructive on the joining device**: the participant's existing local profiles are replaced with the household's profiles. Before joining, the App offers an **Export profiles to file** option so you can save a JSON copy of your current data and re-import later if you change your mind.
- If the owner disbands the household (Settings → Household → Disband) or signs out of iCloud, participants lose live access on their next sync. The local cache of household profiles becomes their own (no destructive wipe on the way out).
- A participant can leave a household at any time (Settings → Household → Leave). Leaving keeps the household's profiles on the participant's device as their own.
- Apple's `CKShare` cap is 100 participants per share. The natural household scale is ~6.

## Export / Import (JSON backup)

In **Settings → Backup** you can:

- **Export profiles to file** — save a JSON file containing every profile on the current device (any household state). Useful as a manual backup or before destructive operations.
- **Import profiles from file** — restore a previous export. **Merge** mode adds missing profiles and updates existing ones if the imported copy is newer. **Replace** mode wipes local profiles and installs the imported set; available only when you're not in a household.

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
- Payment or billing information (purchases are handled entirely by Apple).

## Children's privacy

Spaced Math is designed to be safe for children. Because the App collects no personal information and contacts no third parties, it complies with COPPA's "no personal information" definition. We don't display ads, and there are no accounts or social features. Spaced Math includes a single one-time in-app purchase (an unlock for the full app); because the app is designed for children, a parental gate is shown before any purchase, as Apple's Kids Category rules require. All payments and any promo-code redemptions are handled by Apple through the App Store. The App never sees or stores your payment details.

## Your choices

- **Disable voice mode** at any time per profile (Settings → Voice mode), or globally by denying microphone permission in iOS Settings.
- **Disable iCloud sync** at any time (gear icon → Settings → Sync → Use iCloud → off). Disabling does not delete iCloud copies; delete each profile individually if you want them removed.
- **Disband or leave a household** (Settings → Household → Disband / Leave) to stop sharing. Disbanding revokes participants' access to your household; leaving keeps the household's profiles on your device as your own.
- **Export profiles to a file** (Settings → Backup → Export) and keep it locally — a manual backup that never touches iCloud.
- **Reset a profile's progress** without deleting the profile (per-profile Settings → Reset).
- **Delete a profile** (Manage Profiles → swipe or tap to delete) — also removes the iCloud copy when sync is on. Repeat per profile to remove everything.

## Changes to this policy

If we change this policy, the new version will be available at the same URL with an updated **Last updated** date. Material changes will also be noted in the App's release notes.

## Contact

Questions about this policy or your data? Email **spacedmath@gmail.com**.
