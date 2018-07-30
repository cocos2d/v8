# v8 build

This Repo records v8 build scripts, for cocos2d-x-lite use a specific release of v8 engine. Sometimes we need custom that.

## Steps

### On Android

1. 参考[官方文档](https://github.com/v8/v8/wiki/Building-from-Source) Clone 官方的 V8 仓库
2. 确定版本

    * 重新编译某一平台时需要保持版本一致，直接从当前使用的头文件中取得版本。本次 android 平台使用 clang 重新编译的版本是 6.0.286.52，由于在 `external/android/arm64-v8a/include/v8/v8-version.h` 可以发现
        ```
        #define V8_MAJOR_VERSION 6
        #define V8_MINOR_VERSION 0
        #define V8_BUILD_NUMBER 286
        #define V8_PATCH_LEVEL 52
        ```
    
    * 如果需要整体升级 v8 引擎，请使用 Chrome 最新版本对应的 v8 引擎。比如对于版本 66.0.3359.139，找到 https://chromium.googlesource.com/chromium/src/+/66.0.3359.139 此链接，点击页面中的 `DEPS` 文件，找到 '{chromium_git}/v8/v8.git@512109444cb393dfa6ce32a36f37efde8c4fc5b9' 此字段，确定此稳定版的 Chrome 中使用的 V8 的 commit ID。将 commit ID 累加到 https://github.com/v8/v8/commit/512109444cb393dfa6ce32a36f37efde8c4fc5b9 这个链接，页面打开后，可以确定 V8 的版本为 6.6.346.26

3. 按照官方文档，使用 gclient 同步好代码后，切换到版本对应的 tag，比如 6.0.286.52。切换完 tag 后再执行一次 `gclient sync`，这会同步相关的子仓库到对应的提交。

4. 在 build 目录执行自定义的脚本，`build-android.sh`，顺利完成后，生成的 libs 和头文件将会被放于 v8 目录的 dist-android 文件夹下。

#### 注意

1. 本地环境已经有 ndk 时，不需要再参考 wiki 中的 [D8-on-Android](https://github.com/v8/v8/wiki/D8-on-Android)  执行 `v8$ echo "target_os = ['android']" >> ../.gclient && gclient sync --nohooks` 。执行命令将会下载 NDK，SDK 耗费时间，并且占用非常大的空间。
2. 使用 clang 构建 v8，可以参考 https://chromium.googlesource.com/chromium/src/+/lkcr/docs/clang.md ，能了解到一些构建参数。

## Links

[v8 Repo](https://github.com/v8/v8)

[v8 Wiki](https://github.com/v8/v8/wiki)