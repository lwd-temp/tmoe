# TODO

## tmm

### installation

- 方法 4
  - 工具: apt
  - 平台: tmoe
  - 條件: 您已經添加了 neko/tinor 倉庫
    - 命令 1: ~~`apt install tmm`~~
    - 命令 2: ~~`apt install tmoe-2021`~~
- 方法 5
  - 工具: cargo
  - 平台: crates.io
  - 條件: 您想要手動編譯
    - 命令: ~~`cargo install tmm`~~

### config

運行以下命令

```sh
tmm new uuu ubuntu:kinetic
```

然後它會輸出 "ubuntu:kinetic" 的容器屬性信息（只讀）， 接着會在當前目錄下生成 uuu.toml 配置文件(可寫)。

> 實際配置會比以下內容更加全面，以下內容僅供參考

```toml
name = "uuu"
arch = "arm64"
cmd = ["bash", "-l"]
# user = "root"
user = "0:0"
path = "/xxx/yyy/uuu"

[os]
name = "ubuntu"
code = "kinetic"

[image]
file = "/sdcard/Download/backup/ubuntu-22.10-rootfs.tar.zst"
name = "ubuntu"
tag = "kinetic"
sha256 = "2e72d56249c7b3894d9d5baef5f1fd8fd7aa0fcf8a5253d77ceb7bbfc40d660b"

[mount]
name = [
    "sd",
    "tf",
    "pic",
]

[mount.sd]
enabled = true
type = "bind"
src = "/data/media/0/Download"
dst = "/media/sd"

[mount.pic]
enabled = false

[mount.tf]
enabled = false

[env]
# PATH = ""
# 這是一個小細節，對普通用户和 root 用户使用不同的 PATH。
# 普通用户的 PATH 不應該包含 /sbin
ROOT_PATH = "/usr/local/sbin:/usr/local/bin:/usr/sbin:/sbin:/usr/bin:/bin"
NORMAL_PATH = "/usr/local/bin:/usr/games:/usr/bin:/bin"
```

手動修改這個配置

用 set 子命令修改

```sh
tmm set uuu path "/data/data/xxx/yyy/uuu"
```

用 get 獲取

```sh
tmm get uuu image.tag
# 輸出 kinetic
```

也可以直接修改配置文件。  
最後運行`tmm r uuu` 或者是 `tmm run uuu`