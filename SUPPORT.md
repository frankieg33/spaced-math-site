# Spaced Math — Support

Quick answers to common questions, plus how to get in touch.

## Getting started

1. Open Spaced Math.
2. On the welcome screen, tap **Create Profile**. Pick a name, an emoji, and a color.
3. From the profile home, tap a pile (`+ − × ÷`) or **All operators** to start a study session. Spoken or typed answers both work.

If you've used Spaced Math on another device with iCloud sync on, tap **Restore from iCloud** on the welcome screen instead. Your profiles will appear once iCloud has synced (usually within a few seconds). If you've joined a household on another device, you'll see a confirmation card prompting you to join here too.

## The free app and the full app

Spaced Math is free with one profile and one operation (the one you choose the first time you open the app). A single one-time purchase, the full unlock, adds:

- All four operations plus mixed practice
- Up to 8 profiles, each with its own progress
- Household sharing across your family's devices
- Custom Practice and Time Trials

It is a one-time purchase, not a subscription, and it is shared with your family through Family Sharing.

**How do I unlock the full app?**
Open **Settings → Spaced Math Full → Unlock the full app**, or tap any locked feature. A grown-up solves a quick multiplication problem first (an Apple requirement for children's apps), then the App Store handles payment.

**I already paid. How do I restore it?**
On a new device or after reinstalling, open **Settings → Spaced Math Full → Restore Purchase**, signed in to the App Store with the Apple ID you bought it with. If a family member bought it, Family Sharing unlocks it once you are in the same family group.

**I have a promo or gift code.**
Open **Settings → Spaced Math Full → Redeem a code** and enter it. The full app unlocks as soon as the code is accepted.

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

- A correct answer moves the card further into the future. Faster answers (under 2.0 s by default) get longer intervals.
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
Tap the gear icon on the profile picker → **Settings → Sync → Use iCloud → on**. Make sure you're signed into iCloud in iOS Settings.

**My profiles aren't syncing.**

- Confirm you're signed into iCloud on both devices, and into the *same* Apple ID.
- Confirm sync is on in App Settings on both devices.
- CloudKit cross-device sync is usually fast (seconds, often near-instant via silent push) but can take longer over weak networks. Try opening the App on each device and giving it 30 seconds to settle.

**I switched Apple IDs and now my profiles are gone.**
For your safety, the App detects when the iCloud account on your device changes and turns sync off automatically — so old data isn't silently uploaded to a different account. If your profiles are still on this device, they're untouched. If they were only in the previous iCloud account, switch back to that account and re-enable sync to recover them.

**I want to wipe iCloud copies.**
Open Manage Profiles and delete each profile individually. With iCloud sync enabled, deletes also remove the matching CloudKit records from the family zone.

## Households

Spaced Math supports sharing your entire household with other Apple IDs, so a child using Dad's iPad and Mom's iPhone can pick up exactly where they left off — even when those devices are signed into different iCloud accounts. In v3 the household is the unit of sharing: every profile on the owner's device is part of the household.

**How do I create a household?**

1. Make sure iCloud sync is on (gear icon → Settings → Sync → Use iCloud → on).
2. Open **Settings → Household → Set up household**.
3. Give your household a name (e.g. "Smith family").
4. Pick how to invite people: Messages, Mail, Copy Link, or AirDrop.

**What happens when someone accepts an invite?**

The participant taps the invite link, the App opens with a confirmation sheet, and they choose between:

- **Export first** — saves their current profiles to a JSON file (they can re-import later if they change their mind).
- **Join** — replaces their current profiles with the household's profiles. **This is destructive on the participant's device** — their pre-join profiles are wiped from the device (but not from any iCloud account that already has a copy).
- **Cancel** — does nothing. The user can re-tap the invite link later.

After joining, the participant sees the household name as a chip on their picker and can see + edit any profile in the household. Their study activity writes through CloudKit's permission model to the owner's iCloud.

**Who can see the household?**

Only Apple IDs you explicitly invite. The share is invite-only — anyone with the link can join, but only if you sent it to them. You can revoke access at any time (Settings → Household → Disband).

**Whose iCloud is the data stored in?**

The owner's (the person who created the household). Study activity recorded by any participant writes through CloudKit's permission model to the owner's iCloud. The participant's iCloud doesn't store a separate copy.

**What if the owner disbands the household or signs out of iCloud?**

All participants lose live sync on their next refresh, but the household profiles **stay on their device as their own** — they don't get wiped. If the owner just signed out of iCloud, re-signing in restores live sync for everyone.

**Can a participant leave a household without involving the owner?**

Yes. **Settings → Household → Leave household**. The owner's data is unaffected; the participant keeps the household profiles on their device as their own going forward.

**How many participants can a household have?**

Apple's `CKShare` cap is 100. The natural family scale is around 6 (matches Apple's Family Sharing group max).

**Can a kid under 13 with a managed Apple ID join a household?**

Managed (school-issued) Apple IDs can't be CKShare participants. For those families, sign both devices into the *same* Apple ID instead — the per-Apple-ID sync path still works without invites.

## Export / Import (backup)

In **Settings → Backup** you can:

- **Export profiles to file** — saves every profile on the current device as a JSON file. Useful as a manual off-iCloud backup or before any destructive operation (joining a household, switching devices, etc.).
- **Import profiles from file** — restores a previous export. **Merge** mode adds any missing profiles and updates existing ones if the imported copy has a newer `updatedAt`. **Replace** mode wipes the device's profiles and installs the imported set; available only when you're not currently in a household.

## I want to start a profile over without deleting it

Open the profile, tap the gear icon, then Reset this profile's progress. Clears spaced-repetition state, mistakes, and activity history but keeps the profile's name, emoji, color, and settings.

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
