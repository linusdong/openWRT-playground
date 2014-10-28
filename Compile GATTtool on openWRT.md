# Build GATTtool on openWRT
Please go through openWRT buildroot process first. Click Link [here] (http://wiki.openwrt.nanl.de/doc/howto/buildroot.exigence)

## Prerequisites
0. debian wheezy 32bit i686 OS (best for compiling without errors)
1. [stable SDK OpenWrt 'Attitude Adjustment i686 • ar71xx] (http://downloads.openwrt.org/attitude_adjustment/12.09/ar71xx/generic/OpenWrt-SDK-ar71xx-for-linux-i486-gcc-4.6-linaro_uClibc-0.9.33.2.tar.bz2)
2. arduino yun board
3. CSR4.0 BLE dongle
4. Optional [SDK build from scratch] (https://github.com/arduino/openwrt-yun)
5. go through [this first] (http://wiki.openwrt.nanl.de/doc/howto/obtain.firmware.sdk)

## Build Bluez-4.101
go to buildroot folder and look for bluez folder 
```
feeds/packages/utils/bulez
```
### Change Makefile
Make changes to the following
```
PKG_VERSION:=4.101
DEPENDS:=+libreadline +libncurses +libpthread +libusb +glib2 +dbus +udev $(INTL_DEPENDS) $(ICONV_DEPENDS)
CONFIGURE_ARGS +=--enable-static --enable-gatt --enable-hid2hci --enable-usb --enable-tools --enable-shared

LDFLAGS="$(TARGET_LDFLAGS) -lreadline -lncurses \

$(INSTALL_BIN) $(PKG_INSTALL_DIR)/lib/udev/hid2hci $(1)/lib/udev
$(CP) $(PKG_INSTALL_DIR)/lib/udev/rules.d/* $(1)/lib/udev/rules.d/
```
### Change configure
line 13374, change yes to no
