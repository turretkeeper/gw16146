include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=nrc7292
PKG_RELEASE=1

PKG_SOURCE_URL:=https://github.com/Gateworks/$(PKG_NAME).git
PKG_SOURCE_PROTO:=git
PKG_SOURCE_DATE:=2025-06-03
PKG_SOURCE_VERSION:=f08cbc3f5948ad435c299471ec70050d34f50235
PKG_MIRROR_HASH:=72614cab1612cc56767f9503f692233e68b4667657d3098282ec229b225e7be1

include $(INCLUDE_DIR)/package.mk

define KernelPackage/nrc7292
  SUBMENU:=Network Devices
  TITLE:=NRC7292
  FILES:=$(PKG_BUILD_DIR)/package/src/nrc/nrc.$(LINUX_KMOD_SUFFIX)
  DEPENDS:=+kmod-mac80211
  AUTOLOAD:=$(call AutoLoad,60,nrc7292)
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

define KernelPackage/nrc7292/description
  Driver for Newracom NRC7292 chips
endef

define Build/Compile
	+$(KERNEL_MAKE) modules -C $(LINUX_DIR) M="$(PKG_BUILD_DIR)/package/src/nrc" $(MAKE_FLAGS)
endef

define KernelPackage/nrc7292/install
	mkdir -p $(1)/lib/firmware
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/package/evk/binary/nrc7292_bd.dat $(1)/lib/firmware/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/package/evk/binary/nrc7292_cspi.bin $(1)/lib/firmware/
endef


$(eval $(call KernelPackage,nrc7292))
