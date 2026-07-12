# Desert Thorn Keeper - Publish Checklist

## 1. Project Configuration
- [x] Bundle ID contains 'rosewood': com.rosewood.desertthornkeeper.game
- [x] TARGETED_DEVICE_FAMILY: "1" (iPhone only)
- [x] No iPad support (UIDeviceFamily = 1 only)
- [x] project.yml has no hardcoded signing restrictions
- [x] CODE_SIGN_IDENTITY / CODE_SIGNING_REQUIRED / CODE_SIGNING_ALLOWED removed
- [x] MARKETING_VERSION: "1.0"
- [x] CURRENT_PROJECT_VERSION: "1"
- [x] Deployment target: iOS 15.0

## 2. Info.plist
- [x] CFBundleDisplayName: "Desert Thorn Keeper"
- [x] CFBundleIconName: "AppIcon"
- [x] ITSAppUsesNonExemptEncryption: false
- [x] UILaunchStoryboardName: "LaunchScreen"
- [x] UIRequiredDeviceCapabilities: arm64
- [x] UISupportedInterfaceOrientations: UIInterfaceOrientationPortrait only

## 3. App Icon
- [x] AppIcon.appiconset has all required sizes
- [x] 1024x1024 marketing icon: no Alpha channel
- [x] All icons: no Alpha channel
- [x] Contents.json complete and valid

## 4. Launch Screen
- [x] LaunchScreen.storyboard root tag is `<document>` (lowercase)
- [x] No references to non-existent images (Backgrounds image removed)
- [x] Shows game title "Desert Thorn Keeper"

## 5. Debug UI
- [x] showsFPS = NO
- [x] showsNodeCount = NO

## 6. Template Residue
- [x] No tw_* assets
- [x] No game_01_* assets
- [x] No Template assets
- [x] No Backgrounds.imageset residue

## 7. Screenshots
- [x] screenshots_65/ (1284x2778, 6.5" display) - 4 screenshots
- [x] screenshots_55/ (1242x2208, 5.5" display) - 4 screenshots
- [x] All screenshots: no Alpha channel
- [x] Screenshots show real gameplay

## 8. Release Project
- [x] DesertThornKeeper-ReleaseProject/ created
- [x] Sources synced from DesertThornKeeper/
- [x] project.yml synced (no signing restrictions)
- [x] xcodegen generate successful
- [x] Info.plist has arm64 (not armv7)

## 9. Publish Files
- [x] index.html (uses screenshots_65/ images, /privacy.html link)
- [x] privacy.html (offline, no data collection)
- [x] keywords.txt (92 chars)
- [x] README.md
- [x] GAMEPLAY_FACT_CARD.md
- [x] PUBLISH_CHECKLIST.md (this file)
- [x] appstore-review-text.html
- [x] vercel.json (cleanUrls=false)
- [x] .gitignore (.vercel)

## 10. Archive Build
- [ ] xcodebuild archive with CODE_SIGNING_ALLOWED=NO for verification
- [ ] Verify .app contains: Assets.car, AppIcon*.png, LaunchScreen.storyboardc
- [ ] Verify CFBundleIdentifier = com.rosewood.desertthornkeeper.game
- [ ] Verify CFBundleDisplayName = Desert Thorn Keeper
- [ ] Verify UIDeviceFamily = 1

## 11. GitHub/Vercel Deployment
- [ ] Push publish/DesertThornKeeper/ to GitHub (gh account: a254791905522)
- [ ] Use proxy 127.0.0.1:7897
- [ ] Vercel auto-deploy
- [ ] curl verify index.html live
- [ ] curl verify /privacy.html live (not /privacy)

## 12. App Store Connect
- [ ] App name: Desert Thorn Keeper
- [ ] Bundle ID: com.rosewood.desertthornkeeper.game
- [ ] Support URL: https://desert-thorn-keeper.vercel.app/
- [ ] Privacy Policy URL: https://desert-thorn-keeper.vercel.app/privacy.html
- [ ] Screenshots uploaded (1284x2778 and 1242x2208)
- [ ] Keywords from keywords.txt
- [ ] Description from appstore-review-text.html
