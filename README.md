# expo-dev-launcher does not build on Xcode 27.0

A blank Expo SDK 58 app (`npx create-expo-app@latest --template blank-typescript`) with `expo-dev-client` added (`npx expo install expo-dev-client`). Nothing else is changed, except the bundle identifier in `app.json` so that prebuild does not ask for one.

- expo 58.0.25
- expo-dev-client 58.0.20 (expo-dev-launcher 58.0.20)
- react-native 0.88.1

## Steps

1. Select Xcode 27.0 (27A266a).
2. `npm install`
3. `npx expo prebuild -p ios`
4. `npx expo run:ios`

## Result

The build fails in expo-dev-launcher:

```
node_modules/expo-dev-launcher/ios/SwiftUI/Navigation/DevLauncherToolbar.swift:21:7: error: cannot find 'axisBehavior' in scope
** BUILD FAILED **
```

The call is guarded by `compiler(>=6.4)`, which is also true on Xcode 27.0, whose iOS 27.0 SDK has no `axisBehavior`.
