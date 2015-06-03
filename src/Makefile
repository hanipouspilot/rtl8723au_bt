SHELL := /bin/sh
FW_DIR	:= /lib/firmware/rtl_bt/
MDL_DIR	:= /lib/modules/$(shell uname -r)
DRV_DIR	:= $(MDL_DIR)/kernel/drivers/bluetooth

#Handle the compression option for modules in 3.18+
ifneq ("","$(wildcard $(DRV_DIR)/*.ko.gz)")
COMPRESS_GZIP := y
endif
ifneq ("","$(wildcard $(DRV_DIR)/*.ko.xz)")
COMPRESS_XZ := y
endif

ifneq ($(KERNELRELEASE),)

	obj-m := btusb.o

else
	PWD := $(shell pwd)
	KVER := $(shell uname -r)
	KDIR := /lib/modules/$(KVER)/build

all:
	$(MAKE) -C $(KDIR) M=$(PWD) modules

clean:
	rm -rf *.o *.mod.c *.mod.o *.ko *.symvers *.order *.a
endif

