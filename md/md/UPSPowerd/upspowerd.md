# upspowerd

### 一、要求说明

UPS逻辑要求：
1. 主电池/UPS供电，都能可靠保证平板正常工作，不会异常断电。

2. 状态栏显示UPS电量，低电时红色图标。

3. 系统电量低于5%，自动切换到UPS供电。

4. 主电池取下时，自动切换到UPS.

5. UPS供电时，指示灯亮。

6. 更换主电池后，自动关闭UPS，系统恢复常态运行。   

7. 主电池/UPS同时低电时，系统弹出提示，主电池0%时，系统关机。

8. UPS供电时，更换后的主电池低电，系统弹出提示。

9. 由于UPS可供的持续电流为1.2MA，峰值2A,所以UPS供电时，
   系统提示3分钟倒计时关机，提示请更换电池，同时系统相应的省电。
   
10. 更换主电池后，电量实时变化。


功能控制方法：

  1. 切换到UPS供电：
         echo 1 >/sys/class/gpio/gpio96/value
         echo 1 >/sys/class/gpio/gpio105/value

  2. 切换到主电池供电：  
         echo 0 >/sys/class/gpio/gpio105/value
         echo 0 >/sys/class/gpio/gpio96/value

  3. 切换前，获取UPS电量：

         int batvol  = /sys/devices/platform/tm_common_control/chan3_val
              if(batvol==0)
                  strBak=-1;
              else if(batvol<868)
                 {strBak=0;}
              else if(batvol>=998)
                 {strBak=100;}
              else
                {
                  strBak=((batvol-868)*100/(998-868));
                }

************************
​    batvol 是UPS电量百分比，低于65%，系统显示红色低电图标，禁止从主电池切换到UPS供电。
************************
    4. 切换前，获取主电池电量：
        int batvol  =  /sys/devices/platform/adc_mainbat/chan4_val
       if(batvol<500)
        	ret=0;
       else if(batvol<800)
        	ret=1;
       else if(batvol>=1023)
        	{ret=100;}
        else
        	{
        	ret=((batvol-800)*100/(1023-800));
        	}
****************************
​    batvol 是主电池百分比，小于25%，禁止从UPS切换到主电池供电。
​    UPS供电时，batvol 如果等于0，表示主电池已取出，如果再次大于25，表示用户已更换主电池，需要切换回主电池供电。
****************************
       5. 副电池供电时，锁定主频：
       write 1416000 >/sys/devices/system/cpu/cpu4/cpufreq/scaling_max_freq
       6. 主电池供电时，释放主频
       write 1608000 >/sys/devices/system/cpu/cpu4/cpufreq/scaling_max_freq
       7. 副电池供电时，LED控制：
       echo 1 >/sys/devices/platform/ff3d0000.i2c/i2c-4/4-0062/setLED  亮
       echo 0 >/sys/devices/platform/ff3d0000.i2c/i2c-4/4-0062/setLED  灭
       8. 副电池供电时，背光变暗：
        echo 1 >/sys/devices/platform/backlight/set_brightness_temp 变暗
        echo 0 >/sys/devices/platform/backlight/set_brightness_temp 恢复常态
       9. 获取UPS当前状态：
       读取节点：  /sys/class/gpio/gpio96/value
        高： 当前是UPS供电
        低： 当前是主电池供电

### 二、DBus 接口

1. 查询UPS剩余电量

   ```bash
   dbus-send --system --type=method_call --print-reply --dest=com.syberos.upspower /com/syberos/upspower com.syberos.upspower.GetUPSPowerCapacity
   ```

2. 查询主电池电量

   ```bash
   dbus-send --system --type=method_call --print-reply --dest=com.syberos.upspower /com/syberos/upspower com.syberos.upspower.GetMainPowerCapacity
   ```

3. 查询当前供电所使用的电源类型

   ```bash
   # 1 is UPS, 0 is Main
   dbus-send --system --type=method_call --print-reply --dest=com.syberos.upspower /com/syberos/upspower com.syberos.upspower.GetCurrentPowerType
   ```

   

4. 切换为UPS电源供电

   ```bash
   dbus-send --system --type=method_call --print-reply --dest=com.syberos.upspower /com/syberos/upspower com.syberos.upspower.EnableUPSPower
   ```

   

5. 切换为主电源供电

   ```bash
   dbus-send --system --type=method_call --print-reply --dest=com.syberos.upspower /com/syberos/upspower com.syberos.upspower.EnableMainPower
   ```

6. 监听主电池电量变化

   ```bash
   dbus-monitor --system \ "type='signal',interface='com.syberos.upspower',member='MainPowerCapacityChanged'"
   ```

   

7. 监听UPS电池电量变化

   ```bash
   dbus-monitor --system \ "type='signal',interface='com.syberos.upspower',member='UpsCapacityChanged'"
   ```

   

8. 监听电源类型切换

   ```bash
   dbus-monitor --system \ "type='signal',interface='com.syberos.upspower',member='PowerTypeChanged'"
   ```

   

   