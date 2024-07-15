# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2022 Toco Technologies <info@toco.ae>
#
include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

FAT32_BLOCK_SIZE=1024
FAT32_BLOCKS=$(shell echo $$(($(CONFIG_LITEX_SD_BOOT_PARTSIZE)*1024*1024/$(FAT32_BLOCK_SIZE))))

KERNEL_LOADADDR:=0x80200000

define Build/riscv-sdcard
	rm -f $@.boot #$(KDIR_TMP)/$(IMG_PREFIX)-$(PROFILE)-boot.img
	mkfs.fat $@.boot  -C $(FAT32_BLOCKS)

	#mcopy -i $@.boot $(STAGING_DIR_IMAGE)/$(DEVICE_NAME)-boot.scr ::boot.scr
	#mcopy -i $@.boot $(DTS_DIR)/$(DEVICE_DTS).dtb ::dtb
	mcopy -i $@.boot $(IMAGE_KERNEL) ::Image

	#./gen_sifiveu_sdcard_img.sh \
	#	$@ \
	#	$@.boot \
	#	$(IMAGE_ROOTFS) \
	#	$(CONFIG_LITEX_SD_BOOT_PARTSIZE) \
	#	$(CONFIG_TARGET_ROOTFS_PARTSIZE) \
	#	$(STAGING_DIR_IMAGE)/$(DEVICE_NAME)-u-boot.itb \
	#	$(STAGING_DIR_IMAGE)/$(DEVICE_NAME)-u-boot.itb-spl
endef

define Device/Default
  PROFILES := Default
  KERNEL_NAME := Image
  KERNEL := kernel-bin | libdeflate-gzip
  #IMAGES := sdcard.img.gz
  #IMAGE/sdcard.img.gz := riscv-sdcard | append-metadata | gzip
endef

define Device/litex_arty
  DEVICE_VENDOR := LiteX
  DEVICE_MODEL := arty A35
  #DEVICE_DTS := litex/soc
endef
TARGET_DEVICES += litex_arty

$(eval $(call BuildImage))
