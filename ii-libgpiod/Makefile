#
# Copyright (C) 2018-2019 Michael Heimpold <mhei@heimpold.de>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libgpiod
PKG_VERSION:=1.6.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@KERNEL/software/libs/libgpiod/
PKG_HASH:=841be9d788f00bab08ef22c4be5c39866f0e46cb100a3ae49ed816ac9c5dddc7

PKG_MAINTAINER:=Michael Heimpold <mhei@heimpold.de>
PKG_LICENSE:=LGPL-2.1-or-later
PKG_LICENSE_FILES:=COPYING

PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

ifneq ($(CONFIG_PACKAGE_ii-gpiod-tools),)
CONFIGURE_ARGS += --enable-tools
endif

define Package/ii-libgpiod
  SECTION:=libs
  CATEGORY:=Libraries
  URL:=https://git.kernel.org/pub/scm/libs/libgpiod/libgpiod.git
  TITLE:=Library for interacting with Linux's GPIO character device
  DEPENDS:=@GPIO_SUPPORT
endef

define Package/ii-libgpiod/description
  C library for interacting with the linux GPIO character device
  (gpiod stands for GPIO device).
endef

define Package/ii-gpiod-tools
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Tools for interacting with GPIO pins
  DEPENDS:=+ii-libgpiod
endef

define Package/ii-gpiod-tools/description
  Tools for interacting with the linux GPIO character device
  (gpiod stands for GPIO device).
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/gpiod.h $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgpiod.{so*,a} $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libgpiod.pc $(1)/usr/lib/pkgconfig/
endef

define Package/ii-libgpiod/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgpiod.so.* $(1)/usr/lib/
endef

define Package/ii-gpiod-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,ii-libgpiod))
$(eval $(call BuildPackage,ii-gpiod-tools))
