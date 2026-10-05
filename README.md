# 📶 52140 Bluetooth Fix

Get internet via your phone's Bluetooth tethering.

## Before You Start

- Turn on **Bluetooth tethering** on your phone.
- Make sure **mobile data is ON**.

## Steps

### 1. Kill the conflicting daemon

```sh
killall -9 quec_jio_bt
```

### 2. Pair with your phone

```sh
bluetoothctl
```

Inside `bluetoothctl`:

```
power on
agent on
default-agent
scan on
```

Wait for your phone to appear, then:

```
scan off
pair XX:XX:XX:XX:XX:XX
trust XX:XX:XX:XX:XX:XX
devices Paired
exit
```

### 3. Connect NAP tethering

```sh
busctl call org.bluez /org/bluez/hci0/dev_XX_XX_XX_XX_XX_XX org.bluez.Network1 Connect s nap
```

### 4. Get an IP address

```sh
udhcpc -i bnep0
```

### 5. Test the connection

```sh
ping -c 3 8.8.8.8
```

## Notes

- Replace `XX:XX:XX:XX:XX:XX` (and the underscored version, `XX_XX_XX_XX_XX_XX`) with your phone's actual Bluetooth MAC address.

## Troubleshooting

- **Ping fails?** Check that your phone's mobile data is actually on.
