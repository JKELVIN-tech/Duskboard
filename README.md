# Duskboard

A personal planner and daily tracker for Android. Black and violet, with an animated night-sky background.

## What it does

- **Today**: progress ring, today's schedule, overdue items, daily habits with streaks, a 7-day strip.
- **Planner**: month calendar, list by date, filter by category (add your own categories).
- **Reminders**: choose any mix of *at the time, 1 hour before, morning of (8:00), 1 day before, 2 days before, 1 week before* for each item. They show as real system notifications with a **Mark done** button, even when the app is closed. They are restored after a reboot, app update or clock change.
- **Vault**: store files privately on the phone (PDF, images, Word, Excel, anything).
- **Email**: schedule files to go to the addresses you choose, either at a set time or relative to an event. At that time you get a notification with **Open mail app**, which opens your mail app with the addresses, subject, message and files already filled in. You press send.

## Why email is not fully automatic

Android apps can't send email silently without either the user's mail password or a server. Duskboard does neither, so the last tap is yours. Fully automatic sending needs a small backend that stores the files and sends at the scheduled time. That is a sensible next step.

## Build

Requires JDK 17 and the Android SDK (API 35).

```
./gradlew assembleDebug
```

The APK lands in `app/build/outputs/apk/debug/app-debug.apk`. Or open the folder in Android Studio and press Run.

The repo also has a GitHub Action (`.github/workflows/build.yml`). Push to `main`, open the **Actions** tab, and download the `duskboard-debug-apk` artifact.

## Structure

```
app/src/main/java/com/duskboard/app/
  data/        Room database: items, habits, files, email sends, categories
  reminders/   Alarm scheduling, notifications, boot restore, mail hand-off
  ui/          Jetpack Compose screens, dialogs, theme, animated background
```

## Permissions

- `POST_NOTIFICATIONS` (Android 13+): asked on first launch.
- `SCHEDULE_EXACT_ALARM` (Android 12+): the Today screen shows a banner linking to the setting. Without it, reminders can arrive a few minutes late.
- `RECEIVE_BOOT_COMPLETED`: restores alarms after a restart.

## Status

Written without access to an Android toolchain, so the first build may surface small compile errors. They should be quick fixes.
