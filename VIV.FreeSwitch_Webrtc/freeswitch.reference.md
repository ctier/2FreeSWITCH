###  百问 FreeSwitch(第三版)
第 313 页  

### 1. freeswitch + webrtc
https://freeswitch.org/confluence/display/FREESWITCH/WebRTC

### 2. 公网sturn/trun + webrtc(sipml5)
vi conf/vars.xml (非必须)
```
    <X-PRE-PROCESS cmd="stun-set" data="external_rtp_ip=stun:182.61.xx.25:3478"/>  
    <X-PRE-PROCESS cmd="stun-set" data="external_sip_ip=stun:182.61.xx.25:3478"/>  
```
vi conf/sip_profiles/internal.xml (必须)
```
    <param name="ext-rtp-ip" value="182.61.xx.25"/>
    <param name="ext-sip-ip" value="182.61.xx.25"/>
```
vi conf/sip_profiles/external.xml
```
    <param name="ext-rtp-ip" value="182.61.xx.25"/>
    <param name="ext-sip-ip" value="182.61.xx.25"/>
```

### 3. 内网sturn/trun + webrtc(sipml5)
bug list:

1. No candidate ACL defined Defaulting to wan auto
mod_sofia.c:2342 CODEC NEGOTIATION ERROR 
https://www.cnblogs.com/pangyangqi/p/10240351.html

2. How to Fix G729a CODEC NEGOTIATION ERROR in FreeSWITCH
https://howto.lintel.in/how-to-fix-g729a-codec-negotiation-error-in-freeswitch/


### Verto Phone step-by-step

https://kovalyshyn.pp.ua/1249.html
 

### firefox
sipml5 over ws 可以正常与linphone通话

### chrome
sipml5 over ws 出现个bug, 经查找资料，新本版chrome, 在http下已没有麦克风和摄像头的操作权限，建议走https(wss)协议.
[ERR] switch_rtp.c:3185 audio Handshake failure 1
[INFO] switch_rtp.c:3186 Changing audio DTLS state from HANDSHAKE to FAIL
