include $(TOPDIR)/rules.mk

PKG_NAME:=natmap
PKG_VERSION:=20250721
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/heiher/natmap/releases/download/$(PKG_VERSION)
PKG_HASH:=skip

PKG_MAINTAINER:=Richard Yu <yurichard3839@gmail.com>
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=License

PKG_BUILD_FLAGS:=no-mips16
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/natmap
  SECTION:=net
  CATEGORY:=Network
  TITLE:=TCP/UDP port mapping tool for full cone NAT
  URL:=https://github.com/heiher/natmap
  DEPENDS:=+jq +curl
endef

MAKE_FLAGS += REV_ID="$(PKG_VERSION)"

define Package/natmap/conffiles
/etc/config/natmap
endef

define Package/natmap/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/bin/natmap $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/lib/natmap/
	$(INSTALL_BIN) ./files/natmap-update.sh $(1)/usr/lib/natmap/update.sh
	$(INSTALL_BIN) ./files/natmap-notify.sh $(1)/usr/lib/natmap/notify.sh
	$(INSTALL_BIN) ./files/natmap-forward.sh $(1)/usr/lib/natmap/forward.sh
	$(INSTALL_DIR) $(1)/usr/lib/natmap/plugin-notify
	$(INSTALL_BIN) ./files/telegram_bot.sh $(1)/usr/lib/natmap/plugin-notify
	$(INSTALL_BIN) ./files/pushplus.sh $(1)/usr/lib/natmap/plugin-notify
	$(INSTALL_DIR) $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/qb.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/tr.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/emby.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/cloudflare_origin_rule.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/cloudflare_redirect_rule.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_BIN) ./files/proxy_port.sh $(1)/usr/lib/natmap/plugin
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_CONF) ./files/natmap.config $(1)/etc/config/natmap
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files/natmap.init $(1)/etc/init.d/natmap
endef

$(eval $(call BuildPackage,natmap))
