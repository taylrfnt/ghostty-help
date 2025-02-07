# Build from Source
Sometimes you may want to build from source.  Either there's no package manager binary available, or maybe you want to bisect commits to triage an issue.  This is how you build Ghostty from source.
# MacOS
## Prerequisites
- [x] Install Zig (0.13 is currently required for Ghostty builds, even if there are later versions)
- [x] Install Xcode from the Mac App Store
- [x] Configure Xcode environment
  - [x] VErify you have both the Mac & iOS SDKs installed (Xcode → Settings → Components)
  - [x] Verify the developer directory is `/Applications/Xcode.app/Contents/Developer`
- [x] Clone the Ghostty repo locally (let's call the directory where Ghostty's repo is cloned to `$GHOSTTY_SRC_DIR` for the purposes of this guide)

### Modifying your Xcode developer path
You can view the current develper path using the following command:
```
xcode-select --print-path
```
The output of this command should be `/Applications/Xcode.app/Contents/Developer`.  If it is any other path, it needs to be changed to the proper path.  You can modify it by the following command:
```
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
xcode-select --print-path
```

## Building from Source
If all of the prerequisites above are met, you can begin building from source:
1. Select the commit you wish to build from (using `HEAD` will build the nightly/tip release, or you can set a specific commit).
2. Ensure your current working directory is `$GHOSTTY_SRC_DIR` (the local directory you cloned Ghostty's remote repo to).
3. Run the zig build with the following command:
```
zig build -Doptimize=ReleaseFast
```
4. Wait a few minutes as it compiles and builds.  This might take longer based on your machine's resource limits.
5. After the zig build completes, run the Xcode build to create the `.app` bundle:
```
cd macos && xcodebuild
```
- Once the build completes, it will output something like this:
```
CodeSign /Users/taylor.font/localfiles/ghostty/macos/build/ReleaseLocal/Ghostty.app (in target 'Ghostty' from project 'Ghostty')
    cd /Users/taylor.font/localfiles/ghostty/macos

    Signing Identity:     "Sign to Run Locally"

    /usr/bin/codesign --force --sign - -o runtime --entitlements $GHOSTTY_SRC_DIR/macos/build/Ghostty.build/ReleaseLocal/Ghostty.build/Ghostty.app.xcent --timestamp\=none --generate-entitlement-der $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app

RegisterExecutionPolicyException $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app (in target 'Ghostty' from project 'Ghostty')
    cd $GHOSTTY_SRC_DIR/macos
    builtin-RegisterExecutionPolicyException $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app

Validate $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app (in target 'Ghostty' from project 'Ghostty')
    cd $GHOSTTY_SRC_DIR/macos
    builtin-validationUtility $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app -no-validate-extension -infoplist-subpath Contents/Info.plist

Touch $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app (in target 'Ghostty' from project 'Ghostty')
    cd $GHOSTTY_SRC_DIR/macos
    /usr/bin/touch -c $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app

RegisterWithLaunchServices $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app (in target 'Ghostty' from project 'Ghostty')
    cd $GHOSTTY_SRC_DIR/macos
    /System/Library/Frameworks/CoreServices.framework/Versions/Current/Frameworks/LaunchServices.framework/Versions/Current/Support/lsregister -f -R -trusted $GHOSTTY_SRC_DIR/macos/build/ReleaseLocal/Ghostty.app

** BUILD SUCCEEDED **
```
6. Find your completed `Ghostty.app` bundle in `$GHOSTTY_SRC_DIR/macos/build/ReleaseLocal` and copy it to wherever you keep your applications (ideally `/Applications`).

### Building from a specific commit
If you want to build from a specific commit, you should first identify the commit hash for the commit you wish to build.  Once you have it (let's call it `$COMMIT_HASH`), you can run the following command to check it out into a new local branch (in case you want to make any new commits):
```
git checkout -b build-from-commit ${COMMIT_HASH}
```
After you have successfully checked out this commit on your new local branch, proceed with the steps above to build Ghostty.

### XCFramework Error
```
error: There is no XCFramework found at '$GHOSTTY_SRC_DIR/macos/GhosttyKit.xcframework'. (in target 'Ghostty' from project 'Ghostty')
** BUILD FAILED **
```
This error comes from the `xcodebuild` command.  Odds are you didn't wait for the zig build to complete, something went wrong with the zig build, or maybe you tried to string together all of the build commands into a single entry in your shell and forgot to add some `&&`s.

Try the zig build again by itself and it should result in the following output:
```
TODO ADD ZIG OUTPUT
```
Once you have the zig build completed and can see the `xcframework` contents, you can proceed with the `xcodebuild` from step 5 above.


