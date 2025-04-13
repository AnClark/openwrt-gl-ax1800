#
# Copyright (C) 2021 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# AnClark NOTE:
# ath11k-firmware Repo moved from kvalo to codelinaro.org.
# See https://lists.infradead.org/pipermail/ath10k/2024-March/015344.html for more details.

include $(TOPDIR)/rules.mk

PKG_NAME:=ath11k-firmware
PKG_VERSION:=bc6359cb7ad38b7bc4de6580b7a3c70851c0cafb
PKG_RELEASE:=1

# NOTE: To prevent frequent git clone, download tarball instead.
#PKG_SOURCE_PROTO:=git
#PKG_SOURCE_URL:=https://git.codelinaro.org/clo/ath-firmware/ath11k-firmware.git/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-nodoc.tar.bz2
PKG_SOURCE_URL:=https://git.codelinaro.org/clo/ath-firmware/ath11k-firmware/-/archive/$(PKG_VERSION)
PKG_HASH:=553b921963f5ea34eabd0b99cec60de1d01643fdc138e39abe87018aa75e1b29

PKG_MAINTAINER:=Robert Marko <robimarko@gmail.com>

include $(INCLUDE_DIR)/package.mk

define Package/ath11k-firmware-default
  SECTION:=firmware
  CATEGORY:=Firmware
  URL:=$(PKG_SOURCE_URL)
  DEPENDS:=
endef

define Package/ath11k-firmware-ipq6018
$(Package/ath11k-firmware-default)
  TITLE:=ath11k firmware for IPQ6018 devices
endef

define Package/ath11k-firmware-ipq8074
$(Package/ath11k-firmware-default)
  TITLE:=ath11k firmware for IPQ8074 devices
endef

define Build/Compile
	true
endef

define Package/ath11k-firmware-ipq6018/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/IPQ6018/hw1.0
	$(INSTALL_DIR) $(1)/lib/firmware/IPQ6018
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ6018/hw1.0/2.5.0.1/WLAN.HK.2.5.0.1-01100-QCAHKSWPL_SILICONZ-1/* \
		$(1)/lib/firmware/IPQ6018/
	$(INSTALL_DATA) ./files/board-2.bin.IPQ6018 \
		$(1)/lib/firmware/ath11k/IPQ6018/hw1.0/board-2.bin
	$(INSTALL_DATA) ./files/qdss_trace_config.bin \
		$(1)/lib/firmware/ath11k/IPQ6018/hw1.0/qdss_trace_config.bin
endef

define Package/ath11k-firmware-ipq8074/install
	$(INSTALL_DIR) $(1)/lib/firmware/ath11k/IPQ8074/hw2.0
	$(INSTALL_DIR) $(1)/lib/firmware/IPQ8074
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ8074/hw2.0/board-2.bin \
		$(1)/lib/firmware/ath11k/IPQ8074/hw2.0/
	$(INSTALL_DATA) \
		$(PKG_BUILD_DIR)/IPQ8074/hw2.0/2.5.0.1/WLAN.HK.2.5.0.1-01100-QCAHKSWPL_SILICONZ-1/* \
		$(1)/lib/firmware/IPQ8074/
endef

$(eval $(call BuildPackage,ath11k-firmware-ipq6018))
$(eval $(call BuildPackage,ath11k-firmware-ipq8074))
