include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/version.mk

PKG_NAME:=ath10k-usb-wifi
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
endef

ALLWIFIBOARDS:=
ALLWIFIPACKAGES:=$(foreach BOARD,$(ALLWIFIBOARDS),ath10k-usb-wifi-$(BOARD))

define Package/ath10k-usb-wifi-default
  SUBMENU:=ath10k USB Boarddata
  SECTION:=firmware
  CATEGORY:=Firmware
  DEPENDS:=kmod-ath10k
  TITLE:=Custom Board
endef

define generate-ath10k-usb-wifi-package
  define Package/ath10k-usb-wifi-$(1)
    $(call Package/ath10k-usb-wifi-default)
    TITLE:=Board for $(4)
    CONFLICTS:=$(PREV_BOARD)
  endef

  define Package/ath10k-usb-wifi-$(1)/description
This device custom package adds custom firmware and board-usb.bin
file needed to support QCA9377 USB based devices.

This is package is only necessary for the $(4).
Don't install it for any other device!
  endef

  define Package/ath10k-usb-wifi-$(1)/install-overlay
	$(INSTALL_DIR) $$(1)/lib/firmware/ath10k/QCA9337/hw1.0
	$(INSTALL_DATA) ./$(2) $$(1)/lib/firmware/ath10k/QCA9377/hw1.0/board-usb.bin
  	$(INSTALL_DATA) ./$(3) $$(1)/lib/firmware/ath10k/QCA9377/hw1.0/firmware-5.bin
  endef

  PREV_BOARD+=ath10k-usb-wifi-$(1)
endef

$(eval $(call generate-ath10k-usb-wifi-package,Netgear_WUSB6100M,board-Netgear_WUSB6100M,firmware-Netgear_WUSB6100M,Netgear WUSB6100M))

$(foreach PACKAGE,$(ALLWIFIPACKAGES),$(eval $(call BuildPackage,$(PACKAGE))))
