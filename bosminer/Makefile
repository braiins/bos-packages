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

PKG_NAME:=bosminer
PKG_RELEASE:=1

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

PKG_CONFIG_DEPENDS := \
	CONFIG_EXTERNAL_BOSMINER_BIN_PATH

ifeq ($(strip $(CONFIG_EXTERNAL_BOSMINER_BIN_PATH)),"")
	$(error Empty CONFIG_EXTERNAL_BOSMINER_BIN_PATH)
endif

BOSMINER_BIN_PATH:=$(call qstrip,$(CONFIG_EXTERNAL_BOSMINER_BIN_PATH))

PKG_FILE_DEPENDS := \
	$(BOSMINER_BIN_PATH)

include $(INCLUDE_DIR)/package.mk

define Package/bosminer
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=BOSminer mining software with Stratum V2
  URL:=https://braiins-os.org/
endef

define Package/bosminer/description
 Braiins mining software with Stratum V2 protocol.
endef

define Build/Compile
	true
endef

define Package/bosminer/config
	source "$(SOURCE)/Config.in"
endef

define Package/bosminer/conffiles
/etc/bosminer.toml
/etc/bosminer-power-meter.toml
/etc/bosminer-autotune.json
/etc/bosminer-mri
/etc/bos_license_session
/ect/bos_custom_contract_key
endef

define Package/bosminer/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(BOSMINER_BIN_PATH) $(1)/usr/bin/$(PKG_NAME)
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/bosminer.init $(1)/etc/init.d/$(PKG_NAME)
	$(INSTALL_BIN) ./files/bosminer_detect.init $(1)/etc/init.d/$(PKG_NAME)_detect
endef

$(eval $(call BuildPackage,bosminer))
