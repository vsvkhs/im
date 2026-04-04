首先装好 Linux 系统推荐Debian 11（2022-03-26） （https://laotzu.ftp.acc.umu.se/debian-cd/current/amd64/iso-cd/debian-11.3.0-amd64-netinst.iso）或 Ubuntu LTS
安装编译依赖：                            （2023-04-30） （https://laotzu.ftp.acc.umu.se/debian-cd/current/amd64/iso-cd/debian-11.7.0-amd64-netinst.iso）hyper-v1代额外安装介质选否-nju教育镜像（30+Mbps）软件包流行度调查否xfce桌面（V4.16）（1178个）25分钟左右安装完成。电源管理器关闭锁屏！！

Debian默认是不允许root登录的，   $是普通用户（＃是root用户）
用户普通用户登录,打开终端,输入 命令 su - 回车
sudo apt update -y
sudo apt full-upgrade -y
sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
  bzip2 ccache clang clangd cmake cpio curl device-tree-compiler ecj fastjar flex gawk gettext gcc-multilib \
  g++-multilib git gperf haveged help2man intltool lib32gcc-s1 libc6-dev-i386 libelf-dev libglib2.0-dev \
  libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses5-dev libncursesw5 libncursesw5-dev libreadline-dev \
  libssl-dev libtool lld lldb lrzsz mkisofs msmtp nano ninja-build p7zip p7zip-full patch pkgconf python2.7 \
  python3 python3-pip python3-ply python-docutils qemu-utils re2c rsync scons squashfs-tools subversion swig \
  texinfo uglifyjs upx-ucl unzip vim wget xmlto xxd zlib1g-dev
--------------------------------------------------------------------------------------------------------------
su - vkhs
git clone -b openwrt-24.10 --single-branch https://github.com/immortalwrt/immortalwrt
cd immortalwrt
git clone https://github.com/kiddin9/luci-app-dnsfilter.git package/luci-app-dnsfilter
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig

本app依赖于dnsmasq-full，与OpenWrt默认的dnsmasq冲突，所以编译时请确保已经取消勾选base-system -> dnsmasq

---------------------------
kenzok8一键命令:
sed -i '$a src-git kenzo https://github.com/kenzok8/openwrt-packages' feeds.conf.default
sed -i '$a src-git small https://github.com/kenzok8/small' feeds.conf.default
git pull
./scripts/feeds update -a  未完
./scripts/feeds install -a
make menuconfig
---------------------------
如果需要重新配置：
cd immortalwrt
rm -rf ./tmp && rm -rf .config
make menuconfig
**English** | [中文](https://p3terx.com/archives/build-openwrt-with-github-actions.html)

# Actions-OpenWrt

[![LICENSE](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat-square&label=LICENSE)](https://github.com/P3TERX/Actions-OpenWrt/blob/master/LICENSE)
![GitHub Stars](https://img.shields.io/github/stars/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Stars&logo=github)
![GitHub Forks](https://img.shields.io/github/forks/P3TERX/Actions-OpenWrt.svg?style=flat-square&label=Forks&logo=github)

A template for building OpenWrt with GitHub Actions

## Usage

- Click the [Use this template](https://github.com/P3TERX/Actions-OpenWrt/generate) button to create a new repository.
- Generate `.config` files using [Lean's OpenWrt](https://github.com/coolsnowwolf/lede) source code. ( You can change it through environment variables in the workflow file. )
- Push `.config` file to the GitHub repository.
- Select `Build OpenWrt` on the Actions page.
- Click the `Run workflow` button.
- When the build is complete, click the `Artifacts` button in the upper right corner of the Actions page to download the binaries.

## Tips

- It may take a long time to create a `.config` file and build the OpenWrt firmware. Thus, before create repository to build your own firmware, you may check out if others have already built it which meet your needs by simply [search `Actions-Openwrt` in GitHub](https://github.com/search?q=Actions-openwrt).
- Add some meta info of your built firmware (such as firmware architecture and installed packages) to your repository introduction, this will save others' time.

## Credits

- [Microsoft Azure](https://azure.microsoft.com)
- [GitHub Actions](https://github.com/features/actions)
- [OpenWrt](https://github.com/openwrt/openwrt)
- [coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)
- [Mikubill/transfer](https://github.com/Mikubill/transfer)
- [softprops/action-gh-release](https://github.com/softprops/action-gh-release)
- [Mattraks/delete-workflow-runs](https://github.com/Mattraks/delete-workflow-runs)
- [dev-drprasad/delete-older-releases](https://github.com/dev-drprasad/delete-older-releases)
- [peter-evans/repository-dispatch](https://github.com/peter-evans/repository-dispatch)

## License

[MIT](https://github.com/P3TERX/Actions-OpenWrt/blob/main/LICENSE) © [**P3TERX**](https://p3terx.com)
