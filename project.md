# Keep or Yeet

## What problem am I solving

The gallery on my phone is full of useless photos and videos, and deleting them by hand is so slow and boring that I keep putting it off.

## Who are my users

- **Me** – I have thousands of photos from the last year and a half and want to go through them quickly, in small chunks, over several sessions.
- **Anyone with an Android phone whose gallery keeps piling up** – the app runs locally, no registration needed.

## How I want to solve it (MVP)

A native Android app where I go through photos in batches of 20, dating-app style: swipe right to keep, swipe left to mark for deletion.

```
Pick period and albums → swipe a batch of 20 photos → batch summary → move to trash → restore anything deleted by mistake → next batch
```

MVP features:

1. **Period and album selection** – a date range (default: the last 18 months) and checkable albums (Camera, Screenshots, WhatsApp, ...). The app shows the number of items and their total size.
2. **Card swiping** – right to keep, left to delete. The month, year and album of the photo are shown at the top.
3. **Batches of 20** – the whole selected range is processed batch by batch, and upcoming photos are preloaded.
4. **Back button** – brings back the last card; it can be used repeatedly within the current batch.
5. **Batch summary** – "Delete 7 photos (45 MB)?", with the option to rescue any photo, and a single system confirmation.
6. **Trash and restore** – deleted photos go to the system trash (Android 11+). After each batch a grid of the deleted photos is shown, where I pick the ones I want back.
7. **Progress and resume** – "Batch 14 of 162 · 1.2 GB freed". Decisions are stored on the phone, so I can stop and continue later.
8. **Recently deleted by the app** – an overview of batches from the last 30 days, restoring older photos and "Empty trash".

## What won't be in the MVP (non-goals) and why

| Not in the MVP                                          | Why                                                                                  |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------ |
| **iOS version**                                         | I only need Android; iOS has different rules for gallery access.                     |
| **Publishing on Google Play**                           | A development build is enough for personal use.                                      |
| **Automatic detection of duplicates and similar photos** | Comparing images is a hard problem of its own; in the MVP I decide manually.         |
| **AI quality rating (blurry, bad photos)**              | Adds complexity and cost.                                                            |
| **Filters (videos only) and sorting by size**           | Useful, but not needed to validate the idea; first to add after the MVP.             |
| **Android older than 11**                               | The system trash only exists since Android 11.                                       |
| **Managing photos in Google Photos (cloud)**            | The app only sees and deletes what is physically on the phone.                       |
| **Accounts, sync, social features**                     | The app is purely local and personal.                                                |

## What technologies do I need

- **React Native + Expo + TypeScript** – the app; the same foundation as in my Rastlinnik project.
- **Expo development build** (not Expo Go) – Expo Go has limited gallery access on Android.
- **expo-media-library** – listing albums, loading photos in batches, filtering by album and date.
- **A small native Kotlin module (Expo config plugin)** – moving to trash and restoring via Android MediaStore (Android 11+); `expo-media-library` doesn't offer trash.
- **react-native-gesture-handler + react-native-reanimated** – smooth card swiping.
- **expo-sqlite** – local storage of decisions, position and batch history.
- **Development:** AI coding agents (e.g. Claude Code), Node.js, Git + GitHub; installing the APK directly on the phone.
