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

PKG_NAME:=bos-logger
PKG_RELEASE:=1

PKG_MAINTAINER:=Braiins <braiins@braiins.com>

include $(INCLUDE_DIR)/package.mk

define Package/bos-logger
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Utilities for logging Braiins OS
  DEPENDS:=+logrotate
endef

define Package/bos-logger/description
 Setup and monitor system logs.
endef

define Build/Compile
endef

define Package/bos-logger/install
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/bos-logger.init $(1)/etc/init.d/bos_logger

	$(INSTALL_DIR) $(1)/etc/logrotate.d/
	$(INSTALL_DATA) ./files/system.config $(1)/etc/logrotate.d/system
endef

define Package/bos-logger/preinst
#!/bin/sh

echo "*/1 * * * * /usr/sbin/logrotate /etc/logrotate.conf 2>&1 | logger -t logrotate" \
>> $${IPKG_INSTROOT}/etc/crontabs/root
endef

define Package/bos-logger/postrm
#!/bin/sh

sed -i '/\/usr\/sbin\/logrotate/d' /etc/crontabs/root
/etc/init.d/cron restart
endef

$(eval $(call BuildPackage,bos-logger))
