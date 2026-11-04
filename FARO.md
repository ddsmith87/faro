# Faro

Faro is a private messenger for family and friends, built on a fork of
[FluffyChat](https://github.com/krille-chan/fluffychat) (AGPL-3.0) and the
Matrix protocol. Messages are end-to-end encrypted and live on our own server.

## What has been changed from FluffyChat

| Area | Change |
|---|---|
| Name | "Faro" everywhere users see it: app label, iOS display name, web title, PWA manifest |
| App ID | `us.principlecreation.faro` (Android applicationId, iOS bundle IDs, app groups, URL schemes) |
| Icon | Lighthouse lamp + beam, night navy `#0E1A24` with beam amber `#F2A541` (`assets/logo/img`, `web/icons`) |
| Colors | Fixed Faro grounds (navy dark / sand light) with the beam as accent: `lib/config/themes.dart` → `_faroScheme` |
| Default theme | Dark (`lib/widgets/theme_builder.dart`) |
| Server | Locked to `farochat.live`; other servers disabled (`allowOtherHomeservers = false`, `presetHomeserver`) |
| Welcome text | "A private light for the people you love." |
| CI | FluffyChat's publishing workflows removed; `faro-build.yaml` builds an Android APK and the web app |

## Placeholders to replace

- Domain is set to `farochat.live` in `lib/config/setting_keys.dart`
- GitHub owner is set to `ddsmith87` in `lib/config/app_config.dart`

## Before a public release

1. **Push notifications.** `ios/Runner/GoogleService-Info.plist` is still FluffyChat's Firebase
   project. Create a Faro Firebase project, replace that file, add `android/app/google-services.json`,
   and run a Sygnal push gateway on the Faro server with the same credentials.
2. **Invite-code sign-up screen.** The server requires an invite code (registration token).
   FluffyChat hands that step to a web fallback page; Faro gets a native invite-code field
   matching the approved prototype. Next change after the first CI build passes.
3. **Release signing.** Android builds currently use the debug keystore, which is fine for
   sideloading to family. Add a real keystore via `android/key.properties` before the Play Store.
4. **iOS.** Build on a Mac with Xcode (or a macOS CI runner) under the Apple developer account,
   then TestFlight → unlisted App Store.

## License

Faro is a derivative of FluffyChat and stays under AGPL-3.0. Keep this source public
and linked from the app (`sourceCodeUrl`) so anyone using Faro can get it.
