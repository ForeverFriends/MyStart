# 指纹解锁在OS5.1系统中的应用

## 一、解锁流程



```flow
st=>start: 开始

op=>operation: start lock-screen

serverConnected=>condition: Connect Fingerprint server

waitConnect=>condition: wait for FIngerprint server

noFinger=>operation: 无指纹识别流程


ScreenStatus=>condition: 屏幕是否点亮 
(ScreenDisplayStatus）

ScreenStatus2=>condition: 屏幕是否点亮 
(ScreenDisplayStatus）

setverify=>operation: set server to Identify

verifyresult=>condition: 识别结果

setErrorNum=>operation: set Password ErrorNums 0
setScreenUnlock=>operation: Set ScreenUnlock
gotohomescreen=>operation: enter home-screen

openScreen=>operation: Open Screen

enterpasswordpage=>operation: 输入密码界面
waitScreenDisplay=>operation: 未亮屏状态
等待亮屏
ScreenDisplay=>operation: 点亮屏幕


e=>end: 结束

st->op->serverConnected(no)->waitConnect(no)->noFinger->e 
serverConnected(yes)->setverify->verifyresult(yes)->ScreenStatus(yes)->setErrorNum->setScreenUnlock->e
waitConnect(yes)->setverify
ScreenStatus(no)->openScreen->setScreenUnlock
verifyresult(no)->ScreenStatus2(yes)->enterpasswordpage->noFinger
ScreenStatus2(no)->waitScreenDisplay(right)->ScreenDisplay->enterpasswordpage

```

