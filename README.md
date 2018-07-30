# v8 build

this repo is a mirror of v8/build module, with some custom behavior, for cocos2d-x-lite use a specific release of v8 engine.

## Steps

1. clone v8 repo, you can refer to [v8 official docs](https://github.com/v8/v8/wiki/Building-from-Source)
2. find a release you want to build

    * re-compile only one platform, you can find the version in v8 header `v8-version.h` located at [external](https://github.com/cocos-creator/cocos2d-x-lite-external/tree/next).
        ```
        #define V8_MAJOR_VERSION 6
        ```
    
    * upgrade v8 engine, please select a version that latest stable chrome used. you can refer to [wiki/Version-numbers](https://github.com/v8/v8/wiki/Version-numbers)

3. follow the official docs, sync related sources. and then switch to version tag you want, for example 6.0.286.52. execute `gclient sync` again after checkout version tag, this will reset related repo to corresponding commit.

4. run the custom shell script `build-android.sh`, you will get finally libs and headers in the `v8/dist-android` directory.

## Tips

1. don't need to execute the script below in [wiki/D8-on-Android](https://github.com/v8/v8/wiki/D8-on-Android)

    ```
    v8$ echo "target_os = ['android']" >> ../.gclient && gclient sync --nohooks
    ```
    it will download NDK & SDK, spend much time, and no benific if you have NDK already.

2. build v8 using clang, you can refer to [chromium/clang.md](https://chromium.googlesource.com/chromium/src/+/lkcr/docs/clang.md) to know some build parameters.

## Links

[v8 repo](https://github.com/v8/v8)

[v8 project](https://developers.google.com/v8)