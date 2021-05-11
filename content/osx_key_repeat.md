+++
title = "Disable press and hold keys in OSX"
date = 2021-05-11
[taxonomies]
tags = ["osx", "mac"]

+++

I've been trying out [IntelliJ](https://www.jetbrains.com/idea/) again, along with the IDEAVim plugin. 

Unfortunately when you hold any key (e.g. movement keys) OSX will think you are wanting to insert an accented letter.

To fix this you can apply this system wide setting.

```
defaults write -g ApplePressAndHoldEnabled -bool false
```
You may need to restart IntelliJ for this to take effect

https://stackoverflow.com/questions/39606031/intellij-key-repeating-idea-vim/39733008#39733008
