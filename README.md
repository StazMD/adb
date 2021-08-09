# adb commands that I use in daily work:

```
adb devices - connected devices

adb connect {ip} - connect to device by IP address

adb install path/app.apk - install application
	adb install -e path/app.apk - reinstall app with saved data
	adb install -d path/app.apk - install prev version of app
adb uninstall {название пакета} - uninstall application

adb backup - backup application
	-f - specify a file name and a path where to save backup. By default it would be saved as `backup.ab` in default folder.
	-apk/-noapk - include or not in backup app.apk and data. Not including by default.
	-obb/-noobb - include or not in backup .obb files. Not including by default.
	-shared/-noshared - include or not in backup data from SD card. Not including by default.
	-all - backup all installed apps.
	-system/-nosystem - include or not in backup system applications. Include by default.
	Example: abd backup -nosystem -apk -all -f "C:\apkbackups\backup.ab" 

adb restore {path_to_backup} - restoring backup

adb emu network speed '2g','full','gsm', 'edge', 'hscsd', 'gprs', 'umts', 'hsdpa', 'lte', 'evdo' - set network speed on device

adb shell - Linux shell on device

 df - disk space details
	-h - disk space details in KB/MB format
	/system - for specific folder desk space details. Ex.: adb shell df /system
  du - disk space used by the specified files and subdirectories.
	-h - disk space used by the specified files and subdirectories in KB/MB format
	/system - for specific folder and sub-directories desk space details. Ex.: adb shell du /system

 screencap - screenshot. Example: adb shell screencap /sdcard/screen.png
	adb pull /sdcard/screen.png - pull screenshot file

 screenrecord - video recording
 	--size 1280x720 - screen resolution (if not specified - device's default)
 	--bit-rate 6000000 (6mbit/s)
 	--time-limit 10 - video length
 	--verbose /sdcard/video.mp4 - file path
 		adb pull /sdcard/video.mp4 - push video file

 pm (package manager)
 	list packages - list of installed applications
 		-f - show only system apps
 		-3 - show third-party apps
 		-f - show applications paths
 		-d - show disable apps
 	disable {package_name} - disable app
 	clear {package_name} - clear data
 	uninstall {package_name} - uninstall app

 am (activity manager)
 	start -n {package_name/runner_class} - run app with activity
 	monkey -p {package_name} 1 - run monkey-test in app with 1 action (workaround to run app)
 	force-stop {package_name} - close app
 	start -a android.intent.action.VIEW 'www.google.com' - open browser and Google page

 svc 
 	wifi disable/enable - disable or enable WiFi
 	bluetooth disable/enable - disable or enable Bluetooth
 	power stayon usb - do not turn off the screen when device is plugged in by USB
 	power stayon ac - do not turn off the screen when connected to AC
 	power stayon wireless - do not turn off the screen when connected to WiFi
 	power stayon true - never turn off the screen
 	power reboot - reboot (need root)
 	power shutdown - shut down (need root)

 input
	text 'text' - send text to device
	keyevent 
	tap {x} {y} - send tap to device on coordinates
	swipe - swipe Example: input swipe 10 10 10 1000 - pull down the Notification Panel
	press
	roll

 sh - run scripts files with `.sh` Ex.: adb shell sh /sdcard/file_name.sh

 wm density 420 - change DPI (need root)
 setprop ctl.restart zygote - soft restart
 content insert --uri content://settings/system --bind name:s:status_bar_show_battery_percent --bind value:i:1 - show battery with a percentage icon

logcat - logs in real time
	-V - verbose
	-D - debug
	-I - info
	-W - warnings
	-E - Error Ex.: adb logcat *:E
	-F - fatal
	-S - silent
	-b events - what other apps doing
		adb logcat | findstr com.android.chrome
		
sqlite3 - device database
```