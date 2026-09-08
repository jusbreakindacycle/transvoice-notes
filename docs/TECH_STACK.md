# Technology Stack and Local Preflight

Last updated: 2026-09-09

## Current recommended application stack

Based on current official Expo documentation observed during Phase 0:

- Expo SDK 57 is listed as the latest SDK in the current reference;
- Expo SDK 57 maps to React Native 0.86 and React 19.2.3;
- Expo SDK 57 requires Node.js 22.13.x minimum according to the current SDK table;
- Expo SDK 55+ uses the React Native New Architecture exclusively.

**Important:** Phase 1 must re-check the official documentation immediately before scaffolding. This file is evidence from 2026-09-09, not a permanent version lock.

Preferred stack direction:

- React Native;
- Expo;
- TypeScript;
- Expo Router;
- Expo Development Builds;
- EAS Build/Submit/Update where justified;
- Expo SQLite;
- app-private file storage;
- SecureStore for small secrets;
- custom Expo native module(s) for recording/speech where needed;
- whisper.cpp as primary speech feasibility candidate.

## Expo Go boundary

Expo Go may be used for:

- visual prototype;
- navigation;
- mock data;
- supported JS/Expo APIs.

Do not use Expo Go as evidence for:

- custom native speech;
- production recording reliability;
- SQLCipher;
- real in-app purchases;
- production background audio;
- final performance.

Use a Development Build for those.

## Speech candidate

Current whisper.cpp upstream documentation lists:

- iOS support;
- Android support;
- quantization;
- VAD;
- iOS/Android examples;
- CPU and accelerated paths.

Exact integration approach and model must be benchmarked in Phase 2.

## Local Windows preflight

Run these from the local repository terminal.

Record the real output. Do not install global tools automatically just to make the checklist green.

### Git

```powershell
git status
git branch --show-current
git remote -v
git log --oneline -5
git --version
```

Expected:
- repository is a clone of the GitHub project;
- current local branch is known;
- `origin` is correct;
- no unexpected destructive/uncommitted work.

### Node and package manager

```powershell
node --version
npm --version
where.exe node
where.exe npm
```

If using pnpm/yarn/bun later, record that decision explicitly rather than mixing package managers.

### Java

```powershell
java --version
where.exe java
echo $env:JAVA_HOME
```

Do not pin a JDK version until current Expo/Android build requirements are verified in Phase 1.

### Android SDK / ADB

```powershell
adb version
where.exe adb
echo $env:ANDROID_HOME
echo $env:ANDROID_SDK_ROOT
adb devices -l
```

Also inspect installed SDK platforms/build tools through Android Studio SDK Manager or `sdkmanager` if available.

### Expo/EAS

Do not require permanent global installs if `npx` is sufficient.

Useful checks:

```powershell
npx expo --version
npx eas-cli --version
```

If EAS authentication is needed later, do not paste tokens into repository files or chat logs.

### Disk space

Verify enough free disk space for:

- Android SDK;
- Gradle caches;
- EAS/local artifacts;
- native builds;
- multiple speech models;
- benchmark audio.

### Physical device

For Android Phase 2/4, `adb devices -l` must show the test device when USB debugging is enabled.

iOS device testing through EAS can be planned separately. Deep local Xcode debugging requires macOS access.

## Phase 0 completion rule

Phase 0 cannot be marked `COMPLETE` until the local preflight facts are recorded in `docs/PROJECT_STATE.md`.

If a missing tool is found, classify it:

- blocking now;
- required only in Phase 1;
- required only in Phase 2+;
- optional.

Do not install infrastructure that is not yet needed.
