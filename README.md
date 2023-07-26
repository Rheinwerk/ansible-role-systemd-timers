# systemd-timers

## About
This roles enables you to create systemd timers which call scripts or execute commands.

## Usage

Define a variable ```systemd_timers```. This variable is a dictionary. Every key is a new timer.

### Example

```
systemd_timers:
   example:
      service_ExecStartPre: /bin/bash -c '! /usr/bin/systemctl is-active --quiet other-service.service'
      service_ExecStart: /bin/true
      service_User: ubuntu
      timer_OnCalendar: "*-*-* 23:59:00 CET"
      timer_AccuracySec: 5s
```

### Variables to pass

| Variable | Required |  Default value / Explanation |
|----------|----------|------------------------------|
| service_ExecStartPre | no | Pre-command before command |
| service_ExecStart |  yes | Which command or script to execute |
| service_User | no | Under which users the timer_command is executed. Default: root |
| timer_persistent | no | Takes a boolean argument. If true, the time when the service unit was last triggered is stored on disk. When the timer is activated, the service unit is triggered immediately if it would have been triggered at least once during the time when the timer was inactive. This is useful to catch up on missed runs of the service when the machine was off. Note that this setting only has an effect on timers configured with OnCalendar=. Defaults to false. [Source](https://www.freedesktop.org/software/systemd/man/systemd.timer.html) |
| timer_OnActiveSec | no | Relative time after the timer unit was last activated |
| timer_OnBootSec | no | Relative time after the computer was booted |
| timer_OnStartupSec | no | Relative time after systemd was started |
| timer_OnUnitActiveSec | no | Relative time after the service unit was last activated |
| timer_OnUnitInactiveSec | no | Relative time after the service unit was last deactivated |
| timer_OnCalendar | no | Absolute time when to call activate the unit |
| timer_AccuracySec | no | Timer have a default accuracy of round about one minute. You can set the accuracy with this var. Default: 15s |

More about timers: https://www.freedesktop.org/software/systemd/man/systemd.timer.html

More about timespans: https://www.freedesktop.org/software/systemd/man/systemd.time.html
