# SPDX-License-Identifier: GPL-2.0-only
#
# Copyright (C) 2024 Toco Technologies <info@toco.ae>
#
include $(TOPDIR)/rules.mk

ARCH:=riscv64
BOARD:=litex
BOARDNAME:=LiteX NaxRiscv SoC
FEATURES:=ext4 squashfs
KERNELNAME:=Image
SUBTARGETS:=generic

KERNEL_PATCHVER:=6.6

include $(INCLUDE_DIR)/target.mk

define Target/Description
	Build firmware images for LiteX NaxRiscv boards
endef

$(eval $(call BuildTarget))
