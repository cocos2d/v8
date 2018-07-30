# v8 build

This Repo records v8 build scripts, for cocos2d-x-lite use a specific release of v8 engine. Sometimes we need custom that.

## Steps

### On Android

1. clone v8 Repo, refer to [v8 official docs](https://github.com/v8/v8/wiki/Building-from-Source) , 
2. find a release you want to build

    * re-compile only one platform, you can find the version in v8 header `v8-version.h` which located at [cocos2dx-lite-external](https://github.com/cocos-creator/cocos2d-x-lite-external/tree/next).
        ```
        #define V8_MAJOR_VERSION 6
        #define V8_MINOR_VERSION 0
        #define V8_BUILD_NUMBER 286
        #define V8_PATCH_LEVEL 52
        ```
    
    * upgrade v8 engine, please select v8 version that latest stable Chrome used. you can refer to [wiki/Version-numbers](https://github.com/v8/v8/wiki/Version-numbers)

3. follow the official docs, sync related sources. and then switch to version tag you want, for example 6.0.286.52. to execute `gclient sync` again after checkout version tag, this will reset related repo to corresponding commit.

4. run the custom shell script `build-android.sh`, you will get finally libs and headers in the v8/dist-android directory.

### Attention

1. Don't need to execute the script `v8$ echo "target_os = ['android']" >> ../.gclient && gclient sync --nohooks` in [wiki/D8-on-Android](https://github.com/v8/v8/wiki/D8-on-Android)), it will download NDK & SDK, spend much time, and no benific if you have NDK already.
2. build v8 by clang, you can refer to https://chromium.googlesource.com/chromium/src/+/lkcr/docs/clang.md to know some parameters.

## Links

[v8 Repo](https://github.com/v8/v8)

[v8 Project](https://developers.google.com/v8)