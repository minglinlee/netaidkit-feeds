include $(TOPDIR)/rules.mk

PKG_NAME:=nak-web

PKG_SOURCE_PROTO=git
PKG_SOURCE_URL=https://github.com/msgctl/netaidkit-web.git
PKG_SOURCE_VERSION=1.0

PKG_VERSION:=$(shell cut -c-8 <<< $(PKG_SOURCE_VERSION))
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_SUBDIR=$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
	SECTION:=NetAidKit
	CATEGORY:=NetAidKit
	TITLE:=$(PKG_NAME)
	DEPENDS:=+lighttpd +lighttpd-mod-cgi +nakd
endef

define Package/$(PKG_NAME)/description
	NetAidKit web user interface
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(CP) $(PKG_BUILD_DIR)/nak $(1)/nak
	$(CP) $(PKG_BUILD_DIR)/www $(1)/www
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
