# mali-utgard-3.10
Mali utgard driver with sunxi platform

# How to compile
    git clone --branch r7p0-00rel0 https://github.com/rubitwa/mali-utgard-3.10
    cd mali-utgard-3.10/driver/src/devicedrv/mali
    make ARCH=arm64 KDIR=/usr/src/linux-headers-$(uname -r) USING_DVFS=0 USING_PROFILING=1 USING_DT=1 MALI_PLATFORM=sunxi
    mkdir /lib/modules/$(uname -r)/kernel/extramodules
    cp mali.ko /lib/modules/$(uname -r)/kernel/extramodules
    depmod -a
    modprobe mali

# Compilation problems
      CC [M]  /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_osk_timers.o
      CC [M]  /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_osk_bitmap.o
      CC [M]  /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_memory.o
    In file included from /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/common/mali_timeline.h:19:0,
                     from /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/common/mali_pp_job.h:22,
                     from /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_memory_swap_alloc.h:18,
                     from /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_memory.c:31:
    /usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_sync.h:27:18: fatal error: sync.h: No such file or directory
    #include <sync.h>
                     ^
    compilation terminated.
    scripts/Makefile.build:308: recipe for target '/usr/src/r7p0-00rel0/driver/src/devicedrv/mali/linux/mali_memory.o' failed`

# Simple fix
`ln -s linux/sync.h /usr/src/linux-headers-$(uname -r)/include/sync.h`
