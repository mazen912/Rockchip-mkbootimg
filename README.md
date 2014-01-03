rockchip-mkbootimg
==================

build boot &amp; recovery without android tree (android 4.2.2 )

#
cd Rockchip-mkbootimg

cc -O2 -Wall -Wextra -o mkbootimg mkbootimg.c -lcrypto

cc -O2 -Wall -Wextra -o unpackbootimg unpackbootimg.c

unpackbootimg -i recovery.img
mkbootimg --kernel recovery.img-zImage --ramdisk recovery.img-ramdisk.gz -o recovery_new.img

openssl sha1 recovery.img recovery_new.img

#ramdisk image can be modified like as,

    mkdir ramdisk
    gzip -cd recovery.img-ramdisk.gz | (cd ramdisk && cpio -i)
    # modify files under ramdisk/
    (cd ramdisk && find * | sort | cpio -o -H newc) | gzip > ramdisk_new.gz
    
#    
thanks to fun

http://www.armtvtech.com/armtvtechforum/viewtopic.php?t=212&p=2551#p2554
