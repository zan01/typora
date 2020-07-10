每行的数量

```shell
$ defaults write com.apple.dock springboard-rows -int 9
```

每列的数量

```shell
$ defaults write com.apple.dock springboard-columns -int 8
```

刷新

```shell
$ defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

