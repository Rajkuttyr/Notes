![[Pasted image 20261023220646.png]]![[Pasted image 20261023221113.png]]![[Pasted image 20261023221127.png]]
![[Pasted image 20261023221351.png]]

To restore Google TV later:
```bash
adb shell pm enable --user 0 com.google.android.tvlauncher
adb shell cmd package set-home-activity --user 0 com.google.android.tvlauncher
adb shell input keyevent KEYCODE_HOME
```

To make UPSIDE TV default again:
```bash