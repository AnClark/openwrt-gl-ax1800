#
# Copyright (C) 2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=elfutils
PKG_VERSION:=0.192
PKG_HASH:=616099beae24aba11f9b63d86ca6cc8d566d968b802391334c91df54eab416b4
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:= \
	https://sourceware.org/elfutils/ftp/0.192/
HOST_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/host-build.mk

HOST_CONFIGURE_ARGS += \
	--disable-shared \
	--enable-elf64 \
	--disable-nls

define Host/Configure
        (cd $(HOST_BUILD_DIR)/$(3); \
                $(HOST_CONFIGURE_CMD) \
                $(HOST_CONFIGURE_ARGS); \
        )
endef


define Host/Compile
	+$(MAKE) $(HOST_JOBS) -C $(HOST_BUILD_DIR)
endef

define Host/Install
	$(INSTALL_DIR) $(STAGING_DIR_HOST)/{lib/pkgconfig,include/libelf}
	$(CP) $(HOST_BUILD_DIR)/libelf/{gelf.h,libelf.h,nlist.h} \
						$(STAGING_DIR_HOST)/include/libelf/
	$(CP) $(HOST_BUILD_DIR)/libelf/libelf.a $(STAGING_DIR_HOST)/lib/
	$(CP) $(HOST_BUILD_DIR)/config/libelf.pc $(STAGING_DIR_HOST)/lib/pkgconfig/
endef

define Host/Clean
	rm -rf $(STAGING_DIR_HOST)/include/libelf
	rm -f $(STAGING_DIR_HOST)/lib/libelf.a
	rm -f $(STAGING_DIR_HOST)/lib/pkgconfig/libelf.pc
	$(call Host/Clean/Default)
endef

$(eval $(call HostBuild))
