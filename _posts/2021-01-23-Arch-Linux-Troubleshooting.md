---
layout: post
title: "아치리눅스 설치시 Troubleshooting/설치끝나고 할일"
date: 2021-01-23 00:23:55 +0900
author: JunYoung
categories: CS Linux
tags: Linux Arch_Linux Dual_boot
---

# 윈도우와 듀얼부팅으로 설치 시

## 윈도우는 시스템 시간을 rtc로 리눅스는 utc로 해석해서 서로 시간이 안 맞는다.

```shell
timedatectl set-local-rtc 1
```

을 사용해서 리눅스가 시간을 rtc로 인식하게 바꿔주자.(윈도우를 utc로 인식하게 하려면 레지스트리를
건드려야 한다고 한다)

## grub이 윈도우를 못 잡을시

os-prober를 깔자.

```shell
sudo os-prober
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

boot partition이 윈도우와 리눅스가 서로 다르면
ntfs로 포맷된 윈도우 부트 파티션을 못 읽는다.

```shell
sudo pacman -S ntfs-3g
```

<a href = "https://wiki.archlinux.org/index.php/NTFS-3G" >ntfs-3g</a> 를 깔고 윈도우 파티션을 마운트해준 후 다시 os-prober를 실행시키면 윈도우 파티션을 잡는 것을 볼 수 있다.

# 깔고 우선적으로 할 일

## 마이크로코드 업데이트

```bash
sudo pacman -S amd-ucode (혹은 intel-ucode)
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

# 설치하고 재부팅하기 전에 확인할 점

## 내장그래픽이 없는 CPU

GUI를 사용할 생각이라면 재부팅하기 전 미리 드라이버를 깔아놓자.

## 와이파이를 사용한다면

dhcpcd 또는 networkmanager를 재부팅하기 전 미리 설치해놓자.

기본으로 깔려있지 않아 인터넷을 못 쓰는 사태가 생길 수 있다.(경험담)

# 한글 사용

## 입력기는 uim추천

.xprofile 에

```shell
export GTK_IM_MODULE='uim'
export QT_IM_MODULE='uim'
uim-xim &
export XMODIFIERS='@im=uim'
```

입력(입력기를 uim으로 설정)

```shell
xmodmap -e 'remove mod1 = Alt_R'
xmodmap -e 'keycode 108 = Hangul'
xmodmap -e 'remove control = Control_R'
xmodmap -e 'keycode 105 = Hangul_Hanja'
```

오른쪽 alt를 한글로 설정

<a href = "https://wiki.archlinux.org/index.php/Localization/Korean">참고</a>
