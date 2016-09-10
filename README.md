The whole tree is expecting omnirom 6.0 sources and is a mix of TeamWin (base tree) + jcadduono (extended tree) + steadfasterX (even more extended - omnirom 6.0 compatible, optimized kernel, and fully working decryption).
Prepare the sources from here: https://github.com/omnirom/android/tree/android-6.0

Add to `.repo/local_manifests/idol4_6055k.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <project name="android_device_qcom_sepolicy" path="device/qcom/sepolicy" remote="omnirom" revision="android-6.0" />
  <project name="CyanogenMod/android_device_qcom_common" path="device/qcom/common" remote="github" revision="cm-13.0" />
</manifest>
```

Then run `repo sync` to check it out.


---
Thx 2 celoxocis:

its easy just go into your android/system folder. there is a folder named ".repo" go into there and in its subfolder "local_manifest".
create a file called "manifest.xml" and include the following:
Code:

<?xml version="1.0" encoding="UTF-8"?>
<manifest>
 <remote  name="CyanogenMod"
           fetch="https://github.com/CyanogenMod" />
  <project path="device/qcom/common" name="android_device_qcom_common" remote="CyanogenMod" revision="cm-13.0"/>
  <remove-project path="bootable/recovery" name="android_bootable_recovery" remote="omnirom" revision="android-6.0" groups="pdk-cw-fs"/>
  <project path="bootable/recovery" name="android_bootable_recovery" remote="omnirom" revision="android-7.0" groups="pdk-cw-fs"/>
</manifest>

Note: you can remove the past two lines if you want to stick with TWRP on android-6.0 tree.
Go back into your "android/system" folder. do a "repo sync --force-sync -f"