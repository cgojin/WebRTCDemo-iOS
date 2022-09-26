# WebRTCDemo-iOS
WebRTC iOS example Xcode project.

## Build WebRTC.xcframework

```sh
# Make a work directory
cd $HOME
mkdir work/webrtc
cd work/webrtc

# Building Official Document: https://webrtc.googlesource.com/src/+/refs/heads/main/docs/native-code/development/index.md
# Building script of stasel/WebRTC: https://github.com/stasel/WebRTC/blob/latest/scripts/build.sh
# Download building script of stasel/WebRTC
curl -fsSL -o build.sh https://raw.github.com/stasel/WebRTC/latest/scripts/build.sh
chmod +x build.sh

# Build the WebRTC.xcframework
MACOS=true IOS=true BUILD_VP9=true ./build.sh

# Build WebRTC.xcframework for debugging
MACOS=true IOS=true BUILD_VP9=true DEBUG=true ./build.sh
```

## Import AppRTCMobile to XCode project

This XCode project has been imported the [AppRTCMobile](https://webrtc.googlesource.com/src/+/refs/heads/main/examples/objc/). If you want to create the Xcode project manually, please refer to the following steps.

- Create a new Xcode project and save to $HOME/work/
  - File -> New -> Project... -> iOS -> App
    - Product Name: WebRTCDemo-iOS
    - Language: Objective-C

- Delete all files of WebRTCDemo-iOS group

- Add Files to WebRTCDemo-iOS group
  - Add ../webrtc/src/examples/objc/* to WebRTCDemo-iOS group
    - Added folders: Create groups
    - Add to targets: WebRTCDemo-iOS

  - Delete tests, mac of WebRTCDemo-iOS/AppRTCMobile group.

- Configure targets
    - TARGETS -> WebRTCDemo-iOS -> Build Phases -> Copy Bundle Resources
        Delete the info.plist, fixed building error: Multiple commands produce '.../Info.plist'

    - TARGETS -> WebRTCDemo-iOS -> Build Settings
        - Info.plist File: ../webrtc/src/examples/objc/AppRTCMobile/ios/Info.plist
        - Header Search Paths: "$(SRCROOT)/../webrtc/src" "$(SRCROOT)/../webrtc/src/sdk/objc/base" "$(SRCROOT)/../webrtc/src/examples/objc/AppRTCMobile"
        - Enable Bitcode: No

    - TARGETS -> WebRTCDemo-iOS -> General -> Framework,Librares, and Embedded Content
        Add ../webrtc/src/out/WebRTC.xcframework, and set Embed & Sign.

### License

MIT License - see [LICENSE](LICENSE) for full text
