include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ftdi-usb-spi
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/Gateworks/$(PKG_NAME).git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2025-06-03
PKG_SOURCE_VERSION:=e68c7717e37923cc027cf911adecdb16ca167235
PKG_MIRROR_HASH:=a0bfbf18cb6c7f456ca80005df6ffd5c21fe6222f992446fc6a1325ede69c93b

include $(INCLUDE_DIR)/package.mk

define KernelPackage/ftdi-usb-spi
  SUBMENU:=Network Support
  TITLE:=FTDI USB SPI
  FILES:=$(PKG_BUILD_DIR)/spi-ft232h.$(LINUX_KMOD_SUFFIX)
  DEPENDS:=+kmod-usb-core
  AUTOLOAD:=$(call AutoLoad,50,ftdi-usb-spi)
endef

define KernelPackage/ftdi-usb-spi/description
  Supplementary driver for NRC7292
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) M="$(PKG_BUILD_DIR)" modules
endef

#include $(INCLUDE_DIR)/kernel-defaults.mk

$(eval $(call KernelPackage,ftdi-usb-spi))
