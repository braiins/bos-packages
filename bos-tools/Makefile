# Copyright (C) 2023  Braiins Systems s.r.o.
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

PKG_NAME:=bos-tools
PKG_RELEASE:=1

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

PKG_CONFIG_DEPENDS := \
	CONFIG_EXTERNAL_BOS_TOOLS_BIN_PATH

ifeq ($(strip $(CONFIG_EXTERNAL_BOS_TOOLS_BIN_PATH)),"")
	$(error Empty CONFIG_EXTERNAL_BOS_TOOLS_BIN_PATH)
endif

BOS_TOOLS_BIN_PATH:=$(call qstrip,$(CONFIG_EXTERNAL_BOS_TOOLS_BIN_PATH))

PKG_FILE_DEPENDS := \
	$(BOS_TOOLS_BIN_PATH)

include $(INCLUDE_DIR)/package.mk

define Package/bos-tools
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Utilities for managing Braiins OS
endef

define Package/bos-tools/description
 Add bos script which is used for firmware management.
 It can do factory reset, boot to recovery mode, ...
endef

define Build/Compile
	true
endef

define Package/bos-tools/config
	source "$(SOURCE)/Config.in"
endef

define Package/bos-tools/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./files/bos $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(BOS_TOOLS_BIN_PATH) $(1)/usr/bin/$(PKG_NAME)
endef

$(eval $(call BuildPackage,bos-tools))
