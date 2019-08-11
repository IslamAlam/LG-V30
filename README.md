# LG-V30


[A/B (Seamless) System Updates
](https://source.android.com/devices/tech/ota/ab)

[Partitions and Images
](https://source.android.com/devices/bootloader/partitions-images)

[LG OpenSource Code Distribution
](http://opensource.lge.com/osSch/list?types=ALL&search=H930)

[Implementing A/B Updates
](https://source.android.com/devices/tech/ota/ab/ab_implement)


[gpt.ini](https://android.googlesource.com/device/imagination/creatorci41/+/473abb032f0c5b06c9e1f8da8537309cd9302857/gpt.ini)

[How A/B Partitions and Seamless Updates Affect Custom Development on XDA](https://www.xda-developers.com/how-a-b-partitions-and-seamless-updates-affect-custom-development-on-xda/)



[Bring up Android A/B system (Part 1)
](http://cfig.github.io/2017/03/28/Bring-up-Android-A-B-system/)

[]()


Quote:
1. Android build
- Download original android source code ( android-7.1.2_r4 ) from http://source.android.com
( $repo init -u https://android.googlesource.com/platform/manifest -b android-7.1.2_r4
$repo sync -cdq -j12 --no-tags
$repo start android-7.1.2_r4 --all
)
- Untar opensource packages of LGH930_Nougat_Android.tar.gz into downloaded android source directory
a) tar -xvzf LGH930_Nougat_Android.tar.gz

- And, merge the source into the android source code
- Run following scripts to build android
a) source build/envsetup.sh
b) lunch 1
c) make -j4
- When you compile the android source code, you have to add google original prebuilt source(toolchain) into the android directory.
- After build, you can find output at out/target/product/generic

2. Kernel Build 
- Uncompress using following command at the android directory
a) tar -xvzf LGH930_Nougat_Kernel.tar.gz

- When you compile the kernel source code, you have to add google original "prebuilt" source(toolchain) into the android directory.
- Run following scripts to build kernel

a) cd kernel/msm-4.4
b) mkdir -p out
c) make ARCH=arm64 O=./out joan_global_com_defconfig
d) make ARCH=arm64 O=./out CROSS_COMPILE=$(pwd)/../../prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin/aarch64-linux-android- KERNEL_COMPRESSION_SUFFIX=gz -j4

* "-j4" : The number, 4, is the number of multiple jobs to be invoked simultaneously. 
- After build, you can find the build image(Image.gz) at out/arch/arm64/boot


https://forum.xda-developers.com/lg-v30/development/unofficial-lineageos-14-1-t3740480

    mkdir -p out

    make O=out clean

    make O=out mrproper

    make ARCH=arm64 O=./out joan_global_com_defconfig

    make ARCH=arm64 O=./out KERNEL_COMPRESSION_SUFFIX=gz -j$(nproc --all)

    make ARCH=arm64 O=./out CROSS_COMPILE=$(pwd)/../../../../../toolchain/aarch64-linux-android-4.9/bin/aarch64-linux-android- KERNEL_COMPRESSION_SUFFIX=gz -j$(nproc --all)
