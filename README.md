# htop_android_complie
**//start complie**  
//  
1.**get ncurses library**  
wget http://ftp.gnu.org/gnu/ncurses/ncurses-6.0.tar.gz  
tar -xvf ncurses-6.0.tar.gz  
2.set the compile envs  
export CXX=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-clang++  
export CC=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-clang  
export STRIP=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-strip  
export LD=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-ld  
export AS=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-as  
export AR=/mnt/d/android-ndk-r21e/toolchains/llvm/prebuilt/linux-x86_64/bin/aarch64-linux-android-ar  
export CFLAGS="-fPIE -fPIC -Wno-error -Wno-null-pointer-arithmetic -I/mnt/g/htop_android/ncurses-6.0/install_/include/ncurses -I/mnt/g/htop_android/ncurses-6.0/install_/include"  
export LDFLAGS="-pie -L/mnt/g/htop_android/ncurses-6.0/install_/lib"  
2.**complie ncurses**  
./configure --host=aarch64-linux-android26 --prefix=/mnt/g/htop_android/ncurses-6.0/install_ --with-shared  
make -j4 && sudo make install  
3.**complie htop**  
git clone --recursive https://github.com/htop-dev/htop  
cd htop  
git checkout 3.2.2  
  
fix:  
add LinuxProcessList.c:(.text+0x1400): undefined reference to `ffsl'  
   
in linux/LinuxProcessList.c  
add   #define ffsl __builtin_ffsl in the top  
  
./configure --host=aarch64-linux-android --prefix=/mnt/g/htop_android/htop/install_ --disable-unicode  
make -j4 && sudo make install  
  
3.**add the terminal files sources**  
fix:  
Error opening terminal: xterm-256color  
  
adb push terminfo_  /data/local/tmp/  
  
export TERMINFO=/data/local/tmp/terminfo  
export TERM=xterm-basic  
