# Dynamic Kernel Module Support (DKMS) for the Diolan DLN-2

It seems that some distrobutions, i.e., Fedora, are not providing the [Diolan DLN-2](https://diolan.com/dln-2) kernel modules via the package manager. This repo aims to work around that problem by providing those kernel modules via DKMS.

## Install DKMS

```
sudo cp -R . /usr/src/dln2-5.6.8
sudo dkms install -m dln2 -v 5.6.8
sudo modprobe dln2 gpio-dln2 spi-dln2 i2c-dln2 dln2-adc
```

## Automate inserting modules at boot

```
sudo tee "/etc/modules-load.d/dln2.conf" > /dev/null <<'EOF'
dln2
gpio-dln2
spi-dln2
i2c-dln2
dln2-adc
EOF
```

## Uninstall DKMS

```
sudo dkms uninstall -m dln2 -v 5.6.8
```

## Backup

- [dkms(8) - Linux man page](https://linux.die.net/man/8/dkms)
- [ADXL345 Setup](https://eraretuya.github.io/2017/01/25/adxl345-setup/)
- [New hardware setup using DLN-2 Adapter](https://narcisaam.github.io/Diolan/)
- [systemd: automate modprobe command at boot time](https://unix.stackexchange.com/questions/71064/systemd-automate-modprobe-command-at-boot-time)