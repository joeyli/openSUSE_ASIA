INCLUDES = -I. -I$(KDIR)/include
KBUILD_CFLAGS += -g

all: kernel_modules

obj-m	:= kretprobe_example.o

KDIR    := /lib/modules/$(shell uname -r)/build
PWD    := $(shell pwd)

CFLAGS_kretprobe_example.o = -I$(src)

%.ko: %.o
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) $@

kernel_modules:
	$(MAKE) -C $(KDIR) SUBDIRS=$(PWD) modules

modules_install: all
	install -m 644 kretprobe_example.ko /lib/modules/`uname -r`/kernel/drivers/kretprobe_example.ko
	/sbin/depmod -a

install:	modules_install

clean:
	$(RM) *.o *~ *.ko *.mod.c .*.o.cmd .*.ko.cmd modules.order Module.symvers
	$(RM) -r .tmp_versions
