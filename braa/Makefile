# Copyright (C) 2024  Braiins Systems s.r.o.
#
# This file is part of Braiins Open-Source Initiative (BOSI).
#
# BOSI is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.
#
# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <https://www.gnu.org/licenses/>.
#
# Please, keep in mind that we may also license BOSI or any part thereof
# under a proprietary license. For more information on the terms and conditions
# of such proprietary license or if you have any other questions, please
# contact us at opensource@braiins.com.

include $(TOPDIR)/rules.mk

PKG_NAME:=braa
PKG_RELEASE:=0.82

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

ifeq ($(strip $(CONFIG_EXTERNAL_BRAA_TREE)),"")
    $(error Empty CONFIG_EXTERNAL_BRAA_TREE)
else
    USE_SOURCE_DIR:=$(call qstrip,$(CONFIG_EXTERNAL_BRAA_TREE))
endif

include $(INCLUDE_DIR)/package.mk

define Package/braa
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=braa
endef

define Package/braa/description
 Mass SNMP scanner.
endef

define Package/braa/config
	source "$(SOURCE)/Config.in"
endef

STRIP:=$(TARGET_CROSS)strip

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		STRIP="$(STRIP)"
endef

define Package/braa/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/braa $(1)/usr/bin
endef

$(eval $(call BuildPackage,braa))
