include $(TOPDIR)/rules.mk

PKG_NAME:=nakd

PKG_SOURCE_PROTO=git
PKG_SOURCE_URL=https://github.com/msgctl/netaidkit-nakd.git
PKG_SOURCE_VERSION=51c04c70010ebf5b41b634db0131852d0c69bcfe

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
	DEPENDS:=+lighttpd +lighttpd-mod-cgi +libjson-c +libubus +libubox \
		+libblobmsg-json +libuci +wireless-tools
endef

define Package/$(PKG_NAME)/description
	NetAidKit networking daemon
endef

CONFIGURE_VARS+= \
	CC="$(TOOLCHAIN_DIR)/bin/$(TARGET_CC)"

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/www
	$(INSTALL_DIR) $(1)/run/nakd
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/nakd $(1)/usr/bin/nakd

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/root/etc/init.d/netaidkit \
		$(1)/etc/init.d/netaidkit

	$(INSTALL_DIR) $(1)/usr/share/nakd/scripts
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/root/usr/share/nakd/scripts/* \
		$(1)/usr/share/nakd/scripts
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
# check if we are on real system
if [ -z "$${IPKG_INSTROOT}" ]; then
        echo "Enabling rc.d symlink for netaidkit"
        /etc/init.d/netaidkit enable
fi
exit 0
endef

define Package/$(PKG_NAME)/prerm
#!/bin/sh
# check if we are on real system
if [ -z "$${IPKG_INSTROOT}" ]; then
        echo "Removing rc.d symlink for netaidkit"
        /etc/init.d/netaidkit disable
fi
exit 0
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
