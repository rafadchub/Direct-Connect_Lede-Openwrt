#
# Copyright (C) 2011-2017 Entware
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ptokax
PKG_VERSION:=0.5.2.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_VERSION)-nix-src.tgz
PKG_SOURCE_URL:=http://www.ptokax.org/files
PKG_MD5SUM:=0d5ca7ae81be69eb351fadfd1a498217

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK=$(HOST_TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xzf $(DL_DIR)/$(PKG_SOURCE)

define Package/ptokax
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=P2P
	DEPENDS:=+liblua +libpthread +zlib +libstdcpp +librt
	TITLE:=DC hub
	URL:=http://www.czdc.org/PtokaX/
	MAINTAINER:=Entware team, http://entware.net
endef

define Package/ptokax/description
 PtokaX Direct Connect Hub is a multi-platform server application
 for Neo-Modus Direct Connect Peer-To-Peer sharing network.
endef

TARGET_CFLAGS += -DTIXML_USE_STL
TARGET_LDFLAGS += -ldl

define Build/Compile
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR)/skein $(MAKE_FLAGS)
	$(MAKE_VARS) $(MAKE) -C $(PKG_BUILD_DIR)/tinyxml $(MAKE_FLAGS)
	$(call Build/Compile/Default)
endef

define Package/ptokax/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/PtokaX $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/ptokax $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/root/.PtokaX/cfg
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/cfg.example/*.xml $(1)/root/.PtokaX/cfg
endef

$(eval $(call BuildPackage,ptokax))
