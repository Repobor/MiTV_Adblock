# MiTV_Adblock

#### 已知的广告关联应用

/system/app/MiTVBiAnalytics.apk com.miui.tv.analytics
/system/vendor/app/AdServer.apk com.miui.systemAdSolution
/system/vendor/app/MiTVAdvertise.apk com.xiaomi.mitv.advertise

------

#### 方法

1.无Root

使用adb shell pm uninstall --user 0 $packagename 禁用应用

2.有Root

使用同包名空包替换系统应用 利用 Android 签名限制防止自动升级应用

fake-app是我自己编译的空包，可以直接下载使用

    adb connect 192.168.x.x
    adb push fake-app /data/local/tmp
    adb shell su -c "mount -o rw,remount /system"
    adb shell su -c "mv /system/app/MiTVBiAnalytics.apk /system/app/MiTVBiAnalytics.apk.bak"
    adb shell su -c "mv /system/app/MiTVBiAnalytics.odex /system/app/MiTVBiAnalytics.odex.bak"
    adb shell su -c "mv /system/vendor/app/AdServer.apk /system/vendor/app/AdServer.apk.bak"
    adb shell su -c "mv /system/vendor/app/AdServer.odex /system/vendor/app/AdServer.odex.bak"
    adb shell su -c "mv /system/vendor/app/MiTVAdvertise.apk /system/vendor/app/MiTVAdvertise.apk.bak"
    adb shell su -c "mv /system/vendor/app/MiTVAdvertise.odex /system/vendor/app/MiTVAdvertise.odex.bak"
    adb shell su -c "cp /data/local/tmp/fake-app/MiTVBiAnalytics.apk /system/app/MiTVBiAnalytics.apk"
    adb shell su -c "cp /data/local/tmp/fake-app/AdServer.apk /system/vendor/app/AdServer.apk"
    adb shell su -c "cp /data/local/tmp/fake-app/MiTVAdvertise.apk /system/vendor/app/MiTVAdvertise.apk"
    adb shell su -c "chmod 644 /system/app/MiTVBiAnalytics.apk"
    adb shell su -c "chmod 644 /system/vendor/app/AdServer.apk"
    adb shell su -c "chmod 644 /system/vendor/app/MiTVAdvertise.apk"
