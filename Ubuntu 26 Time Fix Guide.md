# Ubuntu 26 Time Fix Guide (Dual Boot Windows + Ubuntu)

This guide fixes the common problem where:

- Ubuntu time is wrong
- Browser shows wrong time
- Websites show timestamps incorrectly
- Windows and Ubuntu fight over system clock
- Time becomes +6h / -6h incorrect after reboot

This usually happens because:

- Windows stores BIOS time as LOCAL TIME
- Linux stores BIOS time as UTC

When dual booting, they conflict.

---

# Step 1 — Check Current Time Status

Open terminal:

```bash
timedatectl
```

You may see:

```text
RTC in local TZ: no
```

This is usually the cause.

---

# Step 2 — Set Correct Timezone

For Bangladesh:

```bash
sudo timedatectl set-timezone Asia/Dhaka
```

Verify:

```bash
timedatectl
```

Expected:

```text
Time zone: Asia/Dhaka (+06, +0600)
```

---

# Step 3 — Fix Dual-Boot RTC Conflict

IMPORTANT STEP.

Tell Ubuntu to use LOCAL TIME like Windows.

Run:

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

Check again:

```bash
timedatectl
```

Expected:

```text
RTC in local TZ: yes
```

---

# Step 4 — Enable Automatic Internet Time Sync

Enable NTP sync:

```bash
sudo timedatectl set-ntp true
```

Verify:

```bash
timedatectl
```

Expected:

```text
System clock synchronized: yes
NTP service: active
```

---

# Step 5 — Force Correct Timezone Files

Sometimes timezone files are corrupted or cached incorrectly.

Run:

```bash
sudo ln -sf /usr/share/zoneinfo/Asia/Dhaka /etc/localtime
```

Then:

```bash
sudo dpkg-reconfigure -f noninteractive tzdata
```

---

# Step 6 — Reinstall Timezone Database (Important)

```bash
sudo apt update
sudo apt install --reinstall tzdata
```

---

# Step 7 — Force Internet Time Synchronization

Install sync utility:

```bash
sudo apt install ntpdate -y
```

Synchronize:

```bash
sudo ntpdate pool.ntp.org
```

---

# Step 8 — Reboot System

```bash
sudo reboot
```

---

# Step 9 — Verify Everything

After reboot:

```bash
date
```

and:

```bash
timedatectl
```

Expected:

```text
Time zone: Asia/Dhaka (+06, +0600)
RTC in local TZ: yes
System clock synchronized: yes
```

---

# Step 10 — Fix Browser Time Issues

If Ubuntu time is correct but websites still show wrong time:

## Completely close browser

Chrome:

```bash
pkill chrome
```

Brave:

```bash
pkill brave
```

Firefox:

```bash
pkill firefox
```

Then reopen browser.

---

# Step 11 — Verify Browser Timezone

Open:

https://www.whatismybrowser.com/detect/what-timezone-is-my-browser-using

Expected:

```text
Asia/Dhaka
```

---

# Step 12 — Check Browser Console

Press:

```text
F12
```

Open Console and run:

```javascript
Intl.DateTimeFormat().resolvedOptions().timeZone
```

Expected:

```text
Asia/Dhaka
```

Also test:

```javascript
new Date().toString()
```

---

# Step 13 — Hard Refresh Websites

For websites like:

- Polymarket
- Discord
- TradingView
- Crypto sites

Do:

```text
Ctrl + Shift + R
```

or:

- Open DevTools (F12)
- Right click refresh button
- Click:
  "Empty Cache and Hard Reload"

---

# Step 14 — Clear Site Cache (If Needed)

Chrome/Brave:

Settings → Privacy → Site Settings → Stored Data

Remove affected website data.

---

# Step 15 — Disable VPN or Privacy Extensions

Some VPNs/extensions spoof timezone.

Check:

- VPN extensions
- Brave Shields
- Fingerprint protection
- Privacy extensions

Disable temporarily for testing.

---

# Step 16 — Verify Using Another Device

If:

- Ubuntu time is correct
- Browser timezone is correct
- But website still shows old timestamps

Compare with:

- phone
- Windows
- another PC

Some websites use:

- UTC blockchain timestamps
- server-relative time
- cached transaction times

In that case, Ubuntu is NOT the problem anymore.

---

# Useful Commands Summary

## Show time status

```bash
timedatectl
```

## Show current date/time

```bash
date
```

## Set timezone

```bash
sudo timedatectl set-timezone Asia/Dhaka
```

## Fix Windows/Linux dual boot conflict

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

## Enable NTP sync

```bash
sudo timedatectl set-ntp true
```

## Sync internet time

```bash
sudo ntpdate pool.ntp.org
```

## Reconfigure timezone database

```bash
sudo dpkg-reconfigure tzdata
```

---

# Final Notes

This issue is EXTREMELY common on:

- Ubuntu dual boot systems
- Windows + Linux setups
- Fresh Ubuntu installs
- New SSD installations

The main fix is usually:

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

Everything else ensures:

- browser correctness
- NTP sync
- timezone consistency
- website timestamp accuracy

---
```# Ubuntu 26 Time Fix Guide (Dual Boot Windows + Ubuntu)

This guide fixes the common problem where:

- Ubuntu time is wrong
- Browser shows wrong time
- Websites show timestamps incorrectly
- Windows and Ubuntu fight over system clock
- Time becomes +6h / -6h incorrect after reboot

This usually happens because:

- Windows stores BIOS time as LOCAL TIME
- Linux stores BIOS time as UTC

When dual booting, they conflict.

---

# Step 1 — Check Current Time Status

Open terminal:

```bash
timedatectl
```

You may see:

```text
RTC in local TZ: no
```

This is usually the cause.

---

# Step 2 — Set Correct Timezone

For Bangladesh:

```bash
sudo timedatectl set-timezone Asia/Dhaka
```

Verify:

```bash
timedatectl
```

Expected:

```text
Time zone: Asia/Dhaka (+06, +0600)
```

---

# Step 3 — Fix Dual-Boot RTC Conflict

IMPORTANT STEP.

Tell Ubuntu to use LOCAL TIME like Windows.

Run:

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

Check again:

```bash
timedatectl
```

Expected:

```text
RTC in local TZ: yes
```

---

# Step 4 — Enable Automatic Internet Time Sync

Enable NTP sync:

```bash
sudo timedatectl set-ntp true
```

Verify:

```bash
timedatectl
```

Expected:

```text
System clock synchronized: yes
NTP service: active
```

---

# Step 5 — Force Correct Timezone Files

Sometimes timezone files are corrupted or cached incorrectly.

Run:

```bash
sudo ln -sf /usr/share/zoneinfo/Asia/Dhaka /etc/localtime
```

Then:

```bash
sudo dpkg-reconfigure -f noninteractive tzdata
```

---

# Step 6 — Reinstall Timezone Database (Important)

```bash
sudo apt update
sudo apt install --reinstall tzdata
```

---

# Step 7 — Force Internet Time Synchronization

Install sync utility:

```bash
sudo apt install ntpdate -y
```

Synchronize:

```bash
sudo ntpdate pool.ntp.org
```

---

# Step 8 — Reboot System

```bash
sudo reboot
```

---

# Step 9 — Verify Everything

After reboot:

```bash
date
```

and:

```bash
timedatectl
```

Expected:

```text
Time zone: Asia/Dhaka (+06, +0600)
RTC in local TZ: yes
System clock synchronized: yes
```

---

# Step 10 — Fix Browser Time Issues

If Ubuntu time is correct but websites still show wrong time:

## Completely close browser

Chrome:

```bash
pkill chrome
```

Brave:

```bash
pkill brave
```

Firefox:

```bash
pkill firefox
```

Then reopen browser.

---

# Step 11 — Verify Browser Timezone

Open:

https://www.whatismybrowser.com/detect/what-timezone-is-my-browser-using

Expected:

```text
Asia/Dhaka
```

---

# Step 12 — Check Browser Console

Press:

```text
F12
```

Open Console and run:

```javascript
Intl.DateTimeFormat().resolvedOptions().timeZone
```

Expected:

```text
Asia/Dhaka
```

Also test:

```javascript
new Date().toString()
```

---

# Step 13 — Hard Refresh Websites

For websites like:

- Polymarket
- Discord
- TradingView
- Crypto sites

Do:

```text
Ctrl + Shift + R
```

or:

- Open DevTools (F12)
- Right click refresh button
- Click:
  "Empty Cache and Hard Reload"

---

# Step 14 — Clear Site Cache (If Needed)

Chrome/Brave:

Settings → Privacy → Site Settings → Stored Data

Remove affected website data.

---

# Step 15 — Disable VPN or Privacy Extensions

Some VPNs/extensions spoof timezone.

Check:

- VPN extensions
- Brave Shields
- Fingerprint protection
- Privacy extensions

Disable temporarily for testing.

---

# Step 16 — Verify Using Another Device

If:

- Ubuntu time is correct
- Browser timezone is correct
- But website still shows old timestamps

Compare with:

- phone
- Windows
- another PC

Some websites use:

- UTC blockchain timestamps
- server-relative time
- cached transaction times

In that case, Ubuntu is NOT the problem anymore.

---

# Useful Commands Summary

## Show time status

```bash
timedatectl
```

## Show current date/time

```bash
date
```

## Set timezone

```bash
sudo timedatectl set-timezone Asia/Dhaka
```

## Fix Windows/Linux dual boot conflict

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

## Enable NTP sync

```bash
sudo timedatectl set-ntp true
```

## Sync internet time

```bash
sudo ntpdate pool.ntp.org
```

## Reconfigure timezone database

```bash
sudo dpkg-reconfigure tzdata
```

---

# Final Notes

This issue is EXTREMELY common on:

- Ubuntu dual boot systems
- Windows + Linux setups
- Fresh Ubuntu installs
- New SSD installations

The main fix is usually:

```bash
sudo timedatectl set-local-rtc 1 --adjust-system-clock
```

Everything else ensures:

- browser correctness
- NTP sync
- timezone consistency
- website timestamp accuracy

---
```