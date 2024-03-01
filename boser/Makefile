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

PKG_NAME:=boser
PKG_RELEASE:=1

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

PKG_CONFIG_DEPENDS := \
	CONFIG_EXTERNAL_BOSER_BIN_PATH \
	CONFIG_EXTERNAL_BOSER_WWW_PATH \
	CONFIG_EXTERNAL_BOSER_WWW_VAR_PATH

ifeq ($(strip $(CONFIG_EXTERNAL_BOSER_BIN_PATH)),"")
	$(error Empty CONFIG_EXTERNAL_BOSER_BIN_PATH)
endif
ifeq ($(strip $(CONFIG_EXTERNAL_BOSER_WWW_PATH)),"")
	$(error Empty CONFIG_EXTERNAL_BOSER_WWW_PATH)
endif
ifeq ($(strip $(CONFIG_EXTERNAL_BOSER_WWW_VAR_PATH)),"")
	$(error Empty CONFIG_EXTERNAL_BOSER_WWW_VAR_PATH)
endif

BOSER_BIN_PATH:=$(call qstrip,$(CONFIG_EXTERNAL_BOSER_BIN_PATH))
BOSER_WWW_DIR:=$(call qstrip,$(CONFIG_EXTERNAL_BOSER_WWW_PATH))
BOSER_WWW_VAR_DIR:=$(call qstrip,$(CONFIG_EXTERNAL_BOSER_WWW_VAR_PATH))

PKG_FILE_DEPENDS := \
	$(BOSER_BIN_PATH) \
	$(BOSER_WWW_DIR)/ \
	$(BOSER_WWW_VAR_DIR)/

include $(INCLUDE_DIR)/package.mk

define Package/boser
	SECTION:=utils
	CATEGORY:=Utilities
	TITLE:=BOSer
	URL:=https://braiins-os.org/
endef

define Package/boser/description
	Braiins OS backend server
endef

define Build/Compile
	true
endef

define Package/boser/config
	source "$(SOURCE)/Config.in"
endef

define Package/boser/conffiles
/etc/boser.toml
endef

define Package/boser/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(BOSER_BIN_PATH) $(1)/usr/bin/$(PKG_NAME)
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/boser.init $(1)/etc/init.d/boser
	$(INSTALL_DIR) $(1)/www/boser
	$(INSTALL_DIR) $(1)/www/boser/var
	$(CP) -L $(BOSER_WWW_DIR)/* $(1)/www/boser
	chmod -R 0755 $(1)/www/boser
	$(CP) -L $(BOSER_WWW_VAR_DIR)/* $(1)/www/boser/var
	chmod -R 0755 $(1)/www/boser/var
endef

$(eval $(call BuildPackage,boser))
