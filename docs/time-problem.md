# Dual (or multiple) boot time problem
In order to manage time, operating systems need to know two informations
1. The universal time (UTC) and the location, or
2. The local time and the location

Computers have a hardware clock where the time is saved regularly so time can be restored once they are switched on. The time displayed and used by the computer later is either calculated from the universal time and location (1) or reteived directly (2)

Yes, but which time is *stored regularly* in the hardware clock? It depends on the OS
- Linux systems store the UTC in the hardware clock and know the location so they calculate the local time
- Windows stores the local time

Chances are you don't live in a UTC zone, this causes a problem with dual boot computers as each OS when booted will write *its version* of the time. Hopefully, it is possible to fix the problem either by configuring Windows to use UTC or by configuring Linux to use local time.

Here is the way to do it, but please note that in both cases, this requires elevated permissions
## Configuring Windows to use UTC
Create a text file with a ``.reg`` extension with the following contents and then double click on it to merge the contents with the registry
````console
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation]
"RealTimeIsUniversal"=dword:00000001
````
Disable the Windows Time service by typing in a console ``sc config w32time start= disabled``

To cancel the above, change the ``"RealTimeIsUniversal"=dword:00000001`` in the registry file by ``"RealTimeIsUniversal"=-`` and restore the Time service with ``sc config w32time start= demand``
## Configuring Linux to use local time
Run ``timedatectl``, it should return the way Linux is configured. By default, you should find this
````console
RTC in local TZ: no
````
Now run ``timedatectl set-local-rtc 1 --adjust-system-clock`` to change that. Check if the change has been done by running ``timedatectl`` again. You should see this
````console
RTC in local TZ: yes
````
You get the below warning, but I never had a problem related to using local time so far
````console
Warning: The system is configured to read the RTC time in the local time zone.
This mode cannot be fully supported. It will create various problems
with time zone changes and daylight saving time adjustments. The RTC
time is never updated, it relies on external facilities to maintain it.
If at all possible, use RTC in UTC by calling
'timedatectl set-local-rtc 0'.
````
