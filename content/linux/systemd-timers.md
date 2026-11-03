+++
title = 'Replacing Cron with systemd Timers'
date = 2025-09-14T09:00:00Z
description = 'Schedule jobs with systemd timers and get logging, catch-up runs, and jitter for free.'
tags = ['linux', 'systemd', 'tooling']
+++

Cron works, but systemd timers give you logs in the journal, runs that catch
up after the machine was off, and an easy way to test schedules.

## A service and a timer

A timer needs two units: the **service** that does the work, and the
**timer** that decides when it runs.

```ini
# /etc/systemd/system/backup.service
[Unit]
Description=Nightly backup

[Service]
Type=oneshot
ExecStart=/usr/local/bin/backup.sh
```

```ini
# /etc/systemd/system/backup.timer
[Unit]
Description=Run the nightly backup

[Timer]
OnCalendar=*-*-* 02:30:00
Persistent=true
RandomizedDelaySec=10m

[Install]
WantedBy=timers.target
```

- `Persistent=true` runs a missed job at the next boot.
- `RandomizedDelaySec` spreads load when many machines share a schedule.

## Enable and check it

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now backup.timer
systemctl list-timers backup.timer
```

Logs from every run are in the journal:

```bash
journalctl -u backup.service --since today
```

## Test a schedule before using it

```bash
$ systemd-analyze calendar "*-*-* 02:30:00"
```

This prints the normalized form and the next time it will fire, which is much
easier than guessing at cron syntax.
