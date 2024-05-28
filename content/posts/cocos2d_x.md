+++
title = "cocos2d-x"
author = ["PENG Kevin"]
draft = false
+++

## setup {#setup}

1.  download latest version from <https://cocos2d-x.org/download>
2.  edit `~/.bashrc`, add `ANDROID_SDK_ROOT` and `NDK_ROOT`
    and append to `PATH` environment:
    `PATH=$NDK_ROOT:$ANDROID_SDK_ROOT:$PATH`
3.  in file `proj.android`, add
    ```cfg
    sdk.dir=/home/pk/Android/Sdk/
    ndk.dir=/home/pk/Android/Sdk/ndk/19.2.5345600/
    ```
