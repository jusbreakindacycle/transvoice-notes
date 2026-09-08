# Release Checklist

Last updated: 2026-09-09

This is a future gate. Nothing is release-ready yet.

## Product truth

- [ ] README matches implemented capability.
- [ ] No unsupported "AI", accuracy, offline, real-time, encryption, or low-end-device claims.
- [ ] Known limitations are visible.

## Recording

- [ ] Explicit recording action only.
- [ ] Microphone state is obvious.
- [ ] 5-minute physical-device test passed.
- [ ] 30-minute physical-device test passed.
- [ ] 60-minute physical-device test passed or limitation disclosed.
- [ ] Screen lock/background tests passed.
- [ ] Recovery tests passed.
- [ ] Low-storage behavior passed.
- [ ] Audio remains usable after speech failure.

## Speech/language

- [ ] Model license reviewed.
- [ ] Model checksum/install tested.
- [ ] English benchmark completed.
- [ ] Filipino benchmark completed.
- [ ] Taglish benchmark completed.
- [ ] Critical Meaning benchmark completed.
- [ ] User edits remain authoritative.
- [ ] No fake confidence values.

## Privacy/security

- [ ] Privacy policy reflects real flows.
- [ ] Threat model reviewed.
- [ ] No sensitive logs.
- [ ] Secrets scan clean.
- [ ] Permissions minimized.
- [ ] Data deletion tested.
- [ ] Export tested.
- [ ] Cloud retention verified if cloud exists.
- [ ] PIA completed/updated if applicable.

## Platform

### Android
- [ ] Current foreground microphone service requirements verified.
- [ ] Notification behavior verified.
- [ ] Current Play Data Safety declarations reviewed.
- [ ] Current target SDK/store requirements verified.

### iOS
- [ ] AVAudioSession/background behavior verified.
- [ ] Privacy usage descriptions correct.
- [ ] Current App Store privacy declarations reviewed.
- [ ] Current Xcode/iOS SDK submission requirements verified.

## Billing, if present

- [ ] Store-compliant products configured.
- [ ] Restore purchase works.
- [ ] Subscription terms clear.
- [ ] Entitlement sync tested.
- [ ] Duplicate purchase/job paths tested.
- [ ] Account deletion rules satisfied if account exists.

## CI/CD

- [ ] lockfile committed.
- [ ] typecheck passes.
- [ ] lint passes.
- [ ] unit tests pass.
- [ ] DB migrations pass.
- [ ] Android build passes.
- [ ] iOS build passes.
- [ ] runtime/update compatibility verified.
- [ ] rollback plan tested.

## Repository

- [ ] no secrets.
- [ ] no private recordings.
- [ ] third-party notices complete.
- [ ] license strategy explicitly decided.
- [ ] changelog prepared.

## Final evidence

Do not release based solely on simulator/emulator behavior when recording, background audio, or speech performance depends on physical hardware.
