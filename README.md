### Домашнее задание №1 "Базовая настройка коммутатора"
___
#### Цель: Создание сети и настройка основных параметров устройства
___
*Проверяем настройки коммутатора по умолчанию*
```
Switch#show running-config
Building configuration...

Current configuration : 1080 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
```
*Настраиваем базовые параметры коммутатора*
```
Switch#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#no ip domain-lookup
Switch(config)#hostname S1
S1(config)#service password-encryption
S1(config)#enable secret class
S1(config)#banner motd #
Enter TEXT message.  End with the character '#'.
DO NOT ENTER!
#
```
*Назначаем IP-адрес интерфейса SVI на коммутаторе S1*
```
S1#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#interface vlan 1
S1(config-if)#ip address 192.168.1.2 255.255.255.0
S1(config-if)#no shutdown

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up
```
*Ставим пароль для доступ к коммутатору через консоль*
```
S1#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#end
S1#
```
*Настраиваем канал виртуального соединения VTU*
```S1#configure terminal
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#line vty 0
S1(config-line)#exit
S1(config)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login
S1(config-line)#end
```

*Вывод настроенной конфигурации коммутатора*
```
DO NOT ENTER!


User Access Verification

Password: 

S1>enable
Password: 
S1#conf
S1#configure ter
S1#configure terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)# copy running-config startup-config
             ^
% Invalid input detected at '^' marker.
	
S1(config)# copy running-config startup-config
             ^
% Invalid input detected at '^' marker.
	
S1(config)# copy running-config startup-config
             ^
% Invalid input detected at '^' marker.
	
S1(config)# copy running-config
             ^
% Invalid input detected at '^' marker.
	
S1(config)#co
S1(config)#cop
S1(config)#copy
S1(config)#copy
            ^
% Invalid input detected at '^' marker.
	
S1(config)#S1(config)#S1(config)#
S1(config)#
S1(config)#ip default-gateway 192.168.1.1
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#show run
Building configuration...

Current configuration : 1300 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
!
!
!
no ip domain-lookup
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
ip default-gateway 192.168.1.1
!
banner motd ^C
DO NOT ENTER!
^C
!
!
!

line vty 0 15
 password 7 0822455D0A16
 login
!
!
!
!
end
```
*Тестируем сетевое соединение c нашим коммутатором, с помощью утилиты ping*
```
C:\>ping 192.168.1.2

Pinging 192.168.1.2 with 32 bytes of data:

Request timed out.
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255
Reply from 192.168.1.2: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.1.2:
    Packets: Sent = 4, Received = 3, Lost = 1 (25% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```


