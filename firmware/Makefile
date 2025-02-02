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
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=firmware
PKG_MAINTAINER:=Braiins <braiins@braiins.com>

# set firmware version
PKG_RELEASE:=$(if $(DUMP),0,$(call qstrip,$(CONFIG_FIRMWARE_VERSION)))

PKG_CONFIG_DEPENDS := \
	CONFIG_FIRMWARE_MAJOR \
	CONFIG_FIRMWARE_VERSION \
	CONFIG_FIRMWARE_REQUIRE \
	CONFIG_VERSION_PATH

include $(INCLUDE_DIR)/package.mk

define Package/firmware
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Current Firmware
endef

define Package/firmware/description
 Meta package for automated firmware upgrades.
endef

define Package/firmware/config
	source "$(SOURCE)/Config.in"
endef

define Build/Compile
endef

define Package/firmware/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) ./files/fw_info.json $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/opkg
endef

$(eval $(call BuildPackage,firmware))
