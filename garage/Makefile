include $(TOPDIR)/rules.mk

PKG_NAME:=garage
PKG_VERSION:=2.4.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/deuxfleurs-org/garage/archive/v$(PKG_VERSION)/
PKG_HASH:=c1b7aa02c264cac2c1ac88a1c7d0cc6d3265ccd5e29832dee32b6b689addbaf9

PKG_MAINTAINER:=Romain Isnel <ri@frmg.eu>
PKG_LICENSE:=AGPL
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DEPENDS:=rust/host

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/rust/rust-package.mk

export CXX:=$(TARGET_CXX_NOCACHE)
export BINDGEN_EXTRA_CLANG_ARGS:=--sysroot=$(TOOLCHAIN_DIR)

RUSTC_LDFLAGS +=-latomic

define Package/garage
	SECTION:=utils
	CATEGORY:=Utils
	TITLE:=Garage
	URL:=https://garagehq.deuxfleurs.fr/
endef

define Package/garage/description
	Garage is designed for storage clusters composed of nodes running at different physical
	locations, in order to easily provide a storage service that replicates data at these
	different locations and stays available even when some servers are unreachable. Garage
	also focuses on being lightweight, easy to operate, and highly resilient to machine
	failures.
endef

define Package/garage/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/bin/* $(1)/usr/bin
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

define Build/Compile
    $(call Build/Compile/Cargo,src/garage,--no-default-features --features "sqlite bundled-libs")
endef

$(eval $(call RustBinPackage,garage))
$(eval $(call BuildPackage,garage))
