Demonstration of broken `pod lib lint`
======================================

There are two issues, one which can be fixed by forcing a build setting, one which cannot.

## Issue 1: error: double-quoted include in framework header, expected angle-bracketed instead

* Fixed in cocoapods 1.16.0

## Issue 2: error: Sandbox: rsync.samba(44452) deny(1) file-write-create App.app/Frameworks/MyFramework.framework/_CodeSignature (in target 'App' from project 'App')

### Steps to reproduce

* `pod lib lint`

#### Output

```
$ pod lib lint

 -> MyFramework (1.0.0)
    - ERROR | [iOS] xcodebuild: Returned an unsuccessful exit code. You can use `--verbose` for more information.
    - NOTE  | xcodebuild:  note: Using codesigning identity override: -
    - NOTE  | [iOS] xcodebuild:  note: Building targets in dependency order
    - NOTE  | [iOS] xcodebuild:  note: Target dependency graph (3 targets)
    - NOTE  | [iOS] xcodebuild:  note: Signing static framework with --generate-pre-encrypt-hashes (in target 'Pods-App' from project 'Pods')
    - NOTE  | [iOS] xcodebuild:  error: Sandbox: rsync.samba(44452) deny(1) file-write-create /Users/karl.stenerud/Library/Developer/Xcode/DerivedData/App-gnevzkrtpocjzeduklkdbvflsxod/Build/Products/Release-iphonesimulator/App.app/Frameworks/MyFramework.framework/_CodeSignature (in target 'App' from project 'App')
    - NOTE  | [iOS] xcodebuild:  error: Sandbox: rsync.samba(44453) deny(1) file-write-create /Users/karl.stenerud/Library/Developer/Xcode/DerivedData/App-gnevzkrtpocjzeduklkdbvflsxod/Build/Products/Release-iphonesimulator/App.app/Frameworks/MyFramework.framework/.Info.plist.1CvheL (in target 'App' from project 'App')
    - NOTE  | [iOS] xcodebuild:  error: Sandbox: rsync.samba(44453) deny(1) file-write-create /Users/karl.stenerud/Library/Developer/Xcode/DerivedData/App-gnevzkrtpocjzeduklkdbvflsxod/Build/Products/Release-iphonesimulator/App.app/Frameworks/MyFramework.framework/.MyFramework.D0QRCc (in target 'App' from project 'App')
    - NOTE  | [iOS] xcodebuild:  rsync error: some files could not be transferred (code 23) at /AppleInternal/Library/BuildRoots/289ffcb4-455d-11ef-953d-e2437461156c/Library/Caches/com.apple.xbs/Sources/rsync/rsync/main.c(996) [sender=2.6.9]

[!] MyFramework did not pass validation, due to 1 error.
You can use the `--no-clean` option to inspect any issue.
```
