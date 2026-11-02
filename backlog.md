# Keep or Yeet – Initiative, Epics, User Stories

## Initiative

**Reclaim phone storage by clearing my gallery backlog.** Go through the last 18 months of photos and videos (about 3,000 items) and free at least 10 GB within 4 weeks of first using the app.

---

## Epic 1: Choose what to review

**User story 1.1:** As a user, I want to select a date range, so that I only review the period I care about (e.g. the last 18 months).

Tasks:
- Request gallery permission on first launch
- Date range picker with a default of the last 18 months
- Load the number of items and total size for the range

**User story 1.2:** As a user, I want to select which albums to review (Camera, Screenshots, WhatsApp, ...), so that I can start with the albums that hold the most junk.

Tasks:
- List albums with item count and size (expo-media-library)
- Checkbox list of albums, all selected by default
- Combine the album filter with the date range and show the result ("3,240 items, 11 GB")

---

## Epic 2: Swipe through photos

**User story 2.1:** As a user, I want to swipe a photo right to keep it and left to mark it for deletion, so that I can decide in a second.

Tasks:
- Card component with swipe gestures (gesture-handler + reanimated)
- Show month, year and album on the card
- Visual hint for keep / delete while dragging

**User story 2.2:** As a user, I want a Back button, so that I can fix a swipe I made by mistake.

Tasks:
- Keep a stack of decisions for the current batch
- Back button that restores the last card, usable repeatedly

**User story 2.3:** As a user, I want to go through photos in batches of 20, so that the task feels small and I never wait for loading.

Tasks:
- Load photos in pages of 20, oldest first
- Preload the next cards and the next batch
- Option to switch order (newest first)

---

## Epic 3: Delete safely

**User story 3.1:** As a user, I want a summary after each batch ("Delete 7 photos, 45 MB?"), so that I can check my choices before anything is deleted.

Tasks:
- Summary screen with a grid of the photos marked for deletion
- Option to rescue a photo from the list
- Single system confirmation for the whole batch

**User story 3.2:** As a user, I want deleted photos moved to the trash and shown in a grid, so that I can restore any I deleted by mistake.

Tasks:
- Native Kotlin module for moving to trash and restoring (Android MediaStore, Android 11+)
- "Deleted in this batch" screen with selectable photos
- "Restore selected" button with a single system confirmation

**User story 3.3:** As a user, I want to see everything the app deleted in the last 30 days and empty the trash, so that I can restore older photos and actually free the space.

Tasks:
- "Recently deleted by the app" screen grouped by batch
- Restore from an older batch
- "Empty trash" button with a confirmation

---

## Epic 4: Continue later

**User story 4.1:** As a user, I want my progress saved, so that I can stop at any time and continue where I left off.

Tasks:
- Store decisions, current position and batch history in SQLite (expo-sqlite)
- Resume on app start from the saved position
- Do not show photos I already kept

**User story 4.2:** As a user, I want to see my progress and freed space ("Batch 14 of 162, 1.2 GB freed"), so that I stay motivated.

Tasks:
- Progress bar and batch counter
- Running total of freed space
