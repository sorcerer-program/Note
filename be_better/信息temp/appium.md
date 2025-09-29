首先
adb devices
然后，获取当前正在运行的app
adb shell dumpsys window | findstr mCurrentFocus
然后以/划分
前者是app包名，后者是启动的activity

权限
adb shell dumpsys package yh.app.appstart.lg | findstr -i activity
