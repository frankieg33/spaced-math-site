# Spaced Math — Support

Quick answers to common questions, plus how to get in touch.

## Getting started

1. Open Spaced Math.
2. On the welcome screen, tap **Create Profile**. Pick a name, an emoji, and a color.
3. From the profile home, tap a pile (`+ − × ÷`) or **All operators** to start a study session. Spoken or typed answers both work.

If you've used Spaced Math on another device with iCloud sync on, tap **Restore from iCloud** on the welcome screen instead. Your profiles will appear once iCloud has synced (usually within a few seconds).

## Voice mode

By default, the App listens for spoken answers. Numbers can be spoken naturally ("twenty-four", "two four", "one hundred forty-four") or as digits.

**Voice mode isn't working — what now?**

- Make sure you allowed microphone and speech recognition access. iOS Settings → Spaced Math → Microphone (on) and Speech Recognition (on).
- Tap the mic area to discard the current attempt and try again.
- If recognition consistently mishears, switch to the on-screen keypad: tap **Keypad** in the answer area, or open profile Settings → toggle **Voice mode** off.

**My answer is "wrong" but I said the right number.**
Speech recognition can hallucinate a different number than you spoke. If it happens often, switch to the keypad temporarily and let recognition warm up (it tends to improve over time on the same device).

## Spaced repetition

Each profile keeps independent progress. Cards you've never seen are "new" and start due immediately. As you study:

- A correct answer moves the card further into the future. Faster answers (under 1.0 s by default) get longer intervals.
- A wrong answer brings the card right back into rotation: it's re-queued 6–12 cards later in the same session.
- If you recover the card later in the session, only the recovery grade counts — your "mistake" is forgotten.

The **Stats** bar on the profile home shows your streak, total reviews per day, and learned/total cards.

The **Review** card (only visible when there's something to review) is a focused fix-up queue: it cycles through cards you've recently missed, cards in relearning, and cards that are overdue from a previous day.

## Practice (per profile)

The **Practice** bar on the profile home is a no-scheduler free-drill. Same card pool, but ignores due dates. Useful for warming up or for sessions where you don't want to nudge the FSRS scheduler. Practice difficulty (Easy/Medium/Hard) is configurable in Settings.

## Active Numbers

In Settings → Active Numbers, pick which operands (1–12) you want to drill against. The selection acts as a **base**: with `{1, 2}` selected, you'll see every problem touching 1 or 2, not just `1+2` / `2+2` / `1+1`. Toggle a number off and back on without losing its FSRS state.

## iCloud sync

**How do I enable it?**
Settings → iCloud → Use iCloud → on. Make sure you're signed into iCloud in iOS Settings.

**My profiles aren't syncing.**

- Confirm you're signed into iCloud on both devices, and into the *same* Apple ID.
- Confirm sync is on in Settings on both devices.
- Cross-device sync via `NSUbiquitousKeyValueStore` is generally fast (seconds) but can take longer over weak networks. Try opening the App on each device and giving it 30 seconds to settle.

**I switched Apple IDs and now my profiles are gone.**
For your safety, the App detects when the iCloud account on your device changes and turns sync off automatically — so old data isn't silently uploaded to a different account. If your profiles are still on this device, they're untouched. If they were only in the previous iCloud account, switch back to that account and re-enable sync to recover them.

**I want to wipe iCloud copies.**
Open Manage Profiles and delete each profile individually. With iCloud sync enabled, deletes also remove the matching iCloud copies on the same Apple ID.

## I want to start a profile over without deleting it

Settings → Reset this profile's progress. Clears spaced-repetition state, mistakes, and activity history but keeps the profile's name, emoji, color, and settings.

## My device

- Spaced Math runs on iPhone and iPad with iOS 16.0 or later.
- All features work offline, except iCloud sync (requires iCloud sign-in).

## Contact

Email **spacedmath@gmail.com**.

If you've found a bug, please include:

- Your iOS version (Settings → General → About → iOS Version).
- Your device model.
- Whether the issue happens with voice mode, keypad mode, or both.
- A short description of what you expected vs. what happened.

A reply usually goes out within a few days.