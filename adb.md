adb devices - подключенные устройства
adb connect {ip} - подключиться к устройству по IP адресу
adb install path/app.apk - установка приложения
	adb install -e path/app.apk - переустановить с сохранением данных
	adb install -d path/app.apk - установить версию меньше текущей
adb uninstall {название пакета} - удаление приложения
adb backup - бэкап приложения
	-f - указание имя файла и его расположение, куда сохранять. Если не указывать - будет сохранен как backup.ab в каталоге по-умолчанию.
	-apk/-noapk - включать ли в бэкап само приложение или только его данные. По-умолчанию не включает.
	-obb/-noobb - включать ли в бэкап расширения .obb. По-умолчанию не включает.
	-shared/-noshared - включать ли в бэкап содержимое на SD-карте. По-умолчанию не включает.
	-all - необходимость сделать бэкап всех установленных приложений.
	-system/-nosystem - включать ли в бэкап системные приложения. По-умолчанию - включает.
	Example: abd backup -nosystem -apk -all -f "C:\apkbackups\backup.ab" 
adb restore {path_to_backup} - восстановление бэкапа

adb shell - консоль Linux на устройстве
 df - посмотреть занимаемое место
 screencap - сделать скриншот. Example: adb shell screencap /sdcard/screen.png
	adb pull /sdcard/screen.png - вытащить скриншот
 screenrecord - запись видео
 	--size 1280x720 - разрешение экрана (если не указать, будет нативное экрана)
 	--bit-rate 6000000 (6mbit/s)
 	--time-limit 10 - длина видео
 	--verbose /sdcard/video.mp4 - путь
 		adb pull /sdcard/video.mp4 - вытащить виде
 pm (package manager)
 	list packages - список пакетов установленных приложений
 		-f - показать только системные приложения
 		-3 - показать сторонние приложения
 		-f - показать пути установки пакетов
 		-d - показать отключенные приложения
 	disable {package_name} - отключение приложения
 	clear {package_name} - очистка данных
 	uninstall {package_name} - удаление приложения
 am (activity manager)
 	start -n {package_name/runner_class} - запуск приложения с активностью
 	monkey -p {package_name} 1 - запуск манки-теста приложения с 1 действием в приложении (как альтернатива запуска приложения)
 	force-stop {package_name} - закрыть приложение
 	start -a android.intent.action.VIEW 'www.google.com' - открыть браузер и страничку Гугла
 svc 
 	wifi disable/enable - выключить или включить WiFi
 	bluetooth disable/enable - выключить или включить Bluetooth
 	power stayon usb - устройство не выключает экран при подключении к USB
 	power stayon ac - устройство не выключает экран при подключении к зарядке
 	power stayon wireless - устройство не выключает экран при подключении к WiFi
 	power stayon true - устройство не выключает экран никогда
 	power reboot - перезагрузка устройства (требуется root)
 	power shutdown - выключение устройства (требуется root)
 input
	text 'text' - набрать текст на экране
	keyevent 
	tap {x} {y} - тап по координатам
	swipe - свайп Example: input swipe 10 10 10 1000 - вытянуть шторку
	press
	roll
 sh - запуск скриптов с расширением .sh Ex.: adb shell sh /sdcard/имя_файла.sh
 wm density 420 - изменение DPI (требуется root)
 setprop ctl.restart zygote - мягкая перезагрузка
 content insert --uri content://settings/system --bind name:s:status_bar_show_battery_percent --bind value:i:1 - батарейка в процентах

logcat - логи в реальном времени
	-V - verbose
	-D - debug
	-I - info
	-W - warnings
	-E - Error Ex.: adb logcat *:E
	-F - fatal
	-S - silent
	-b events - что делают другие приложения
		adb logcat | findstr com.android.chrome
sqlite3 - работа с базой данных телефона

