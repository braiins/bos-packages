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

PKG_NAME:=espflash
PKG_RELEASE:=1.5.0
HOST_USE_NINJA:=0

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

ifeq ($(strip $(CONFIG_EXTERNAL_ESPFLASH_TREE)),"")
    $(error Empty CONFIG_EXTERNAL_ESPFLASH_TREE)
else
    USE_SOURCE_DIR:=$(call qstrip,$(CONFIG_EXTERNAL_ESPFLASH_TREE))
endif

CMAKE_SOURCE_SUBDIR:=/examples/bmm_example
CMAKE_BINARY_SUBDIR:=/examples/bmm_example

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/espflash
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Utility for flashing ESP32 Wi-Fi
endef

define Package/espflash/description
 Espessif flash utility
endef

define Package/espflash/config
	source "$(SOURCE)/Config.in"
endef

STRIP:=$(TARGET_CROSS)strip

define Package/espflash/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/examples/bmm_example/bmm_flasher $(1)/usr/bin/espflash
endef

$(eval $(call BuildPackage,espflash))
