include $(ROOTDIR)/rules.mk

PKG_NAME:=xray
PKG_VERSION:=25.5.16

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/XTLS/Xray-core/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=c856cd9abed7d28d3c7b856c0661cec5c85ba0669affa740c979cf40c2f73ee4

PKG_BUILD_DIR:=$(BUILD_DIR)/Xray-core-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Build/Configure
endef

define Build/Compile
	(cd $(PKG_BUILD_DIR); \
		GOOS=linux GOARCH=mipsle CGO_ENABLED=0 \
		go build -v -o xray \
		-trimpath -ldflags "-s -w -buildid=" \
		./main; \
	)
endef

$(eval $(call BuildPackage,xray))

romfs:
	$(INSTALL_DIR) $(ROMFSDIR)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/xray $(ROMFSDIR)/usr/bin/xray
