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

PKG_NAME:=mmc-utils-ii
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://git.kernel.org/pub/scm/utils/mmc/mmc-utils.git
PKG_SOURCE_DATE:=2022-01-16
PKG_SOURCE_VERSION:=3969aa4804edb8aed7bcb3c958e49d0c7388b067
PKG_MIRROR_HASH:=a9ad550e5cc2cae54facb000a1d5e98c41215ccaca439cec6ffddc9fd595f269

PKG_LICENSE:=GPL-2.0-only
PKG_LICENSE_FILES:=

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

include $(INCLUDE_DIR)/package.mk

define Package/mmc-utils-ii
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Userspace tools for MMC/SD devices with Braiins patches
  URL:=https://git.kernel.org/pub/scm/utils/mmc/mmc-utils.git
endef

define Package/mmc-utils-ii/description
  This package contains the userspace mmc utils, the userspace
  counterpart to the Linux MMC/SD subsystem.

  The patches includes:
  * new command 'enh_attrs' for direct access to 'PARTITIONS_ATTRIBUTE'
endef

define Build/Configure
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
	        $(TARGET_CONFIGURE_OPTS) CFLAGS="$(TARGET_CFLAGS) -U_FORTIFY_SOURCE -D_FORTIFY_SOURCE=2" \
	        mmc
endef

define Package/mmc-utils-ii/install
	$(INSTALL_DIR) $(1)/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mmc $(1)/sbin
endef

$(eval $(call BuildPackage,mmc-utils-ii))
