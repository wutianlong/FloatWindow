# FloatWindow
===========

like 360 phone assistent,send rocket from bottom of the window,show the current memory
consume

## Demo show
![FloatWindowDemo](https://github.com/wutianlong/FloatWindow/blob/master/floatwindow.gif)

## Self Define WindowManager

manage smallRocketWindow,BigButtonWindow,RocketLaunchWindow, for example: 1.WindowManager.addView(View,LayoutParmas); 2.WindowManager.removeView(View); 3.WindowManager.updateViewLayout(View,LayoutParmas);
    	
         /**
	 * 创建一个小悬浮窗。初始位置为屏幕的右部中间位置。
	 */
	public static void createSmallWindow(Context context) {
		WindowManager windowManager = getWindowManager(context);
		int screenWidth = windowManager.getDefaultDisplay().getWidth();
		int screenHeight = windowManager.getDefaultDisplay().getHeight();
		if (smallWindow == null) {
			smallWindow = new FloatWindowSmallView(context);
			if (smallWindowParams == null) {
				smallWindowParams = new LayoutParams();
				smallWindowParams.type = LayoutParams.TYPE_SYSTEM_ALERT;
				smallWindowParams.format = PixelFormat.RGBA_8888;
	   			smallWindowParams.flags = LayoutParams.FLAG_NOT_TOUCH_MODL
						| LayoutParams.FLAG_NOT_FOCUSABLE;
				smallWindowParams.gravity = Gravity.LEFT | Gravity.TOP;
				smallWindowParams.width = FloatWindowSmallView.windowViewWidth;
				smallWindowParams.height = FloatWindowSmallView.windowViewHeight;
				smallWindowParams.x = screenWidth;
				smallWindowParams.y = screenHeight / 2;
			}
			smallWindow.setParams(smallWindowParams);
			windowManager.addView(smallWindow, smallWindowParams);
		}
	}

## Get Total Memory

read the file: "/proc/meminfo",file content below:

    /proc/meninfo   中内容如下：
	MemTotal:        2069356 kB
	MemFree:         1492220 kB
	Buffers:            6128 kB
	Cached:           278740 kB
	SwapCached:            0 kB
	Active:           318988 kB
	Inactive:         226652 kB
	Active(anon):     260784 kB
	Inactive(anon):      436 kB
	Active(file):      58204 kB
	Inactive(file):   226216 kB
	Unevictable:           0 kB
	Mlocked:               0 kB
	HighTotal:       1187784 kB
	HighFree:         641068 kB
	LowTotal:         881572 kB
	LowFree:          851152 kB
	SwapTotal:             0 kB
	SwapFree:              0 kB
	Dirty:                 0 kB
	Writeback:             0 kB
	AnonPages:        260736 kB
	Mapped:            96272 kB
	Shmem:               468 kB
	Slab:              16452 kB
	SReclaimable:       6584 kB
	SUnreclaim:         9868 kB
	KernelStack:        3328 kB
	PageTables:         5308 kB
	NFS_Unstable:          0 kB
	Bounce:                0 kB
	WritebackTmp:          0 kB
	CommitLimit:     1034676 kB
	Committed_AS:   13144452 kB
	VmallocTotal:     122880 kB
	VmallocUsed:       45556 kB
	VmallocChunk:      49660 kB
	HugePages_Total:       0
	HugePages_Free:        0
	HugePages_Rsvd:        0
	HugePages_Surp:        0
	Hugepagesize:       4096 kB
	DirectMap4k:       16376 kB
	DirectMap4M:      892928 kB

## Service always running

Timer.sheduleAtFixedRate(TimeTask,delay,period);
