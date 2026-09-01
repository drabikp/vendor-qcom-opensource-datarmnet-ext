KERNEL_SRC ?= /lib/modules/$(shell uname -r)/build

KBUILD_OPTIONS := RMNET_SHS_ROOT=$(PWD)
KBUILD_OPTIONS += MODNAME?=rmnet_shs
# NOTE: KBUILD_EXTRA_SYMBOLS below uses := (immediate expansion), so this MUST
# be defined ABOVE it -- a later assignment is captured too late. It is also
# passed as a bare GOAL in the all: recipe, so an empty value yields
# ".../offload/../..//Module.symvers" and "No rule to make target".
# Motorola's Android.mk supplies this; kernel.mk does not.
DATARMNET_CORE_PATH ?= datarmnet/core
KBUILD_EXTRA_SYMBOLS := $(M)/../../$(DATARMNET_CORE_PATH)/Module.symvers
M ?= $(shell pwd)

all:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) modules $(KBUILD_OPTIONS) $(KBUILD_EXTRA_SYMBOLS)

modules_install:
	$(MAKE) INSTALL_MOD_STRIP=1 -C $(KERNEL_SRC) M=$(M) modules_install

clean:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) clean

# ---- arcfox kernel.mk port ----
KBUILD_OPTIONS += KCPPFLAGS="-DCONFIG_RMNET_LA_PLATFORM -DRMNET_TRACE_INCLUDE_PATH=$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet/core -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet/core -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet-ext/mem -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/dataipa/drivers/platform/msm/include -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/dataipa/drivers/platform/msm/include/uapi"
KBUILD_OPTIONS += KBUILD_EXTRA_SYMBOLS="$(OUT_DIR)/../sm8635-modules/qcom/opensource/datarmnet/core/Module.symvers $(OUT_DIR)/../sm8635-modules/qcom/opensource/datarmnet-ext/mem/Module.symvers"
