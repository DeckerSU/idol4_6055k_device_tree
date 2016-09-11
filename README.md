History of changes
------------------

- 11.09.2016
  - Added correct time in TWRP recovery. 
  - Demo video: https://www.youtube.com/watch?v=TOIpFEiQ65w
  - Fix adopted storage mount. Now all mounts correctly.
  - Fix userdata decryption. Now all works fine. Problem was in qseecomd wouldn't start, now it fixed. 

- 10.09.2016

This TWRP builds and works fine, except decryption of userdata partition.

Initially probles with decryption was described here: http://forum.xda-developers.com/showpost.php?p=68618351&postcount=2257
And here all needed logs (included dmesg, logcat, and recovery logs): http://forum.xda-developers.com/showpost.php?p=68621748&postcount=2262

Thx to steadfasterX and celoxocis for advices.

Some notes for myself:
----------------------

How to add local manifest with CM13 device/qcom/common sources?

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

---

How to push github commit?

git add .
git commit -m "comment"
git push -u origin master

--- 

Useful topics
-------------

- http://forum.xda-developers.com/showthread.php?p=68621748
- http://forum.xda-developers.com/showpost.php?p=68249027&postcount=3
- http://stackoverflow.com/questions/33779286/selinux-policy-definition-for-android-system-service-how-to-setup
- https://github.com/TeamWin/Team-Win-Recovery-Project/issues/477
- https://github.com/TeamWin/android_device_oneplus_oneplus2/issues/1 (qseecomd start problem)
- http://forum.xda-developers.com/showthread.php?t=2794413 (Blob utility)
- https://github.com/omnirom/android_device_huawei_angler/blob/android-6.0/recovery/root/init.recovery.angler.rc (interesting solution to make qseecomd work in recovery)
