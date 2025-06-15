include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ftdi-usb-spi
PKG_RELEASE:=1

PKG_SOURCE_URL:=https://github.com/Gateworks/ftdi-usb-spi.git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2025-06-03
PKG_SOURCE_VERSION:=e68c7717e37923cc027cf911adecdb16ca167235
PKG_MIRROR_HASH:=a0bfbf18cb6c7f456ca80005df6ffd5c21fe6222f992446fc6a1325ede69c93b

include $(INCLUDE_DIR)/package.mk

define KernelPackage/usb-ftdi-spi
  SUBMENU:=USB Support
  TITLE:=FTDI FT232H SPI controller
  FILES:=$(PKG_BUILD_DIR)/spi-ft232h.$(LINUX_KMOD_SUFFIX)
  DEPENDS:=+kmod-usb-core
  AUTOLOAD:=$(call AutoLoad,50,spi-ft232h)
endef

GCC_VERSION=$(shell echo "$(CONFIG_GCC_VERSION)" | sed 's/[^0-9.]*\([0-9.]*\).*/\1/')

MAKE_FLAGS+= \
	TARGET_NAME=$(CONFIG_TARGET_NAME) \
	TOOL_PATH=$(firstword $(TOOLCHAIN_BIN_DIRS)) \
	SYS_PATH=$(LINUX_DIR) \
	TOOLPREFIX=$(TARGET_CROSS) \
	KVER=$(LINUX_VERSION) \
	KDIR=$(LINUX_DIR) \
	ARCH=$(LINUX_KARCH) \
	TARGET_SUFFIX=$(CONFIG_TARGET_SUFFIX) \
	GCC_VERSION=$(GCC_VERSION) \
	EXTRA_CFLAGS="-fno-stack-protector -I$(STAGING_DIR)/usr/include" \
	SoC=$(CONFIG_TARGET_SUBTARGET) \
	SHELL="$(BASH)"

define KernelPackage/usb-ftdi-spi/description
  FT232H supports SPI in MPSSE mode. This driver provides MPSSE
  SPI controller in master mode.
endef

include $(INCLUDE_DIR)/kernel-defaults.mk

define Build/Compile
	+$(MAKE) modules -C $(PKG_BUILD_DIR) $(MAKE_FLAGS)
endef

$(eval $(call KernelPackage,usb-ftdi-spi))
