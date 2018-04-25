---
layout: post
title: SSH 대신 Mosh를 쓰자!
description: "SSH 대신 Mosh를 쓰자!"
tags: [ssh, mosh]
---

<div style="text-align: center;">
  <img src="https://mosh.org/mosh.png" alt="Mosh">
</div>

<br>

[mosh.org](https://mosh.org/)에서는 Mosh를 이렇게 설명하고 있습니다.

```
Remote terminal application that allows roaming, supports intermittent connectivity, and provides intelligent local echo and line editing of user keystrokes.
```

로밍을 허용하고, 간헐적인 연결성을 지원한다고 합니다.

로밍이라는 건 `Wi-Fi`에서 `Ethernet`으로 전환된다거나 하는, 네트워크 전환을 말합니다.

```
Mosh is a replacement for SSH. It's more robust and responsive, especially over Wi-Fi, cellular, and long-distance links.
```

Mosh는 SSH를 대체하고. Wi-Fi, 셀룰러 및 장거리 연결에 좋다고 하네요.

Mosh를 사용하기 위해서는 2가지 준비가 필요합니다.

  * 서버 컴퓨터에 Mosh 설치
  * 60000~61000 UDP 포트 허용

Ubuntu 16.04를 기준으로 다음 한 줄이면 설치가 됩니다.

```bash
sudo apt install mosh
```

<br>

다음으로 60000~61000 UDP 포트를 허용해줘야 합니다.

![ipTime Port Forwarding](https://i.imgur.com/phQd3zi.png)

<br>

준비가 끝났으면 클라이언트를 실행시킵니다.

[mosh.org](https://mosh.org/#getting)에서 지원하는 플랫폼을 확인하고 설치할 수 있습니다.

Windows는 [Chrome 확장 프로그램](https://chrome.google.com/webstore/detail/mosh/ooiklbnjmhbcgemelgfhaeaocllobloj)으로 쓸 수 있고, Android는 [JuiceSSH](https://play.google.com/store/apps/details?id=com.sonelli.juicessh)에서 쓸 수 있습니다.

![Mosh Client for Chrome](https://i.imgur.com/xs2CRSb.png)

<div style="text-align: center;">Mosh Client for Chrome</div>

<br>

`Username`, `Hostname`, `SSH port`를 입력하고 Connect 버튼을 누르면 됩니다. 여기서 SSH 포트를 적게 되는데, 연결할 때만 SSH를 쓰고 연결 이후에는 세션을 만들어 UDP 통신을 하는 것 같습니다.
