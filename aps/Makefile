#By default build for CLD
RMNET_APS_SELECT := CONFIG_RMNET_APS=m
KBUILD_OPTIONS += $(RMNET_APS_SELECT)
KBUILD_OPTIONS += $(KBUILD_EXTRA) # Extra config if any
KBUILD_EXTRA_SYMBOLS := $(M)/../../$(DATARMNET_CORE_PATH)/Module.symvers

M ?= $(shell pwd)

all:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) modules $(KBUILD_OPTIONS)

modules_install:
	$(MAKE) INSTALL_MOD_STRIP=1 -C $(KERNEL_SRC) M=$(M) modules_install

clean:
	$(MAKE) -C $(KERNEL_SRC) M=$(M) clean

# ---- arcfox kernel.mk port ----
KBUILD_OPTIONS += KCPPFLAGS="-DCONFIG_RMNET_LA_PLATFORM -DRMNET_TRACE_INCLUDE_PATH=$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet/core -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet/core -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/datarmnet-ext/mem -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/dataipa/drivers/platform/msm/include -I$(KERNEL_SRC)/../sm8635-modules/qcom/opensource/dataipa/drivers/platform/msm/include/uapi"
KBUILD_OPTIONS += KBUILD_EXTRA_SYMBOLS="$(OUT_DIR)/../sm8635-modules/qcom/opensource/datarmnet/core/Module.symvers $(OUT_DIR)/../sm8635-modules/qcom/opensource/datarmnet-ext/mem/Module.symvers"
