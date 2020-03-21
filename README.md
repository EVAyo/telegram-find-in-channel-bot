# [@FindInChannelBot](https://telegram.me/FindInChannelBot)

Telegram 的消息搜索功能不支持中日韩等语言，因为这类语言字词间不加空格。而我习惯于使用 Telegram 的频道做笔记，因此一个好用的搜索功能对我来说很重要。为了能方便地在频道内搜索，这个机器人诞生了。

The ‘Find in Conversations’ feature in Telegram does not support searching in Chinese/Japanese/Korean etc., since these languages do not have spaces between words. I'm used to take note in Telegram channels, so it's important for me to have a better search tool. So I made this bot so I can find in channels easily.

## Usage

`/start` 启用
`/add`  添加频道，建立信息库
`/find` 搜索
`/cancel` 取消会话

## 依赖
- python3
- sqilte3
- git
## 部署
这里以 CentOS7 为例进行部署。其他系统暂未尝试，欢迎补充

### 1. 安装依赖
安装 python3
```sh
yum install Python3
```
安装 Sqlite3
```sh
yum install sqlite-devel
```
安装 git
```sh
yum install git
```

### 2. 获取Telegram api 和 Bot Taken
这个机器人使用的并不是 HTTP bot API，而是 MTProto 客户端 API。请先获取这两样东西：

* App `api_id` 和 `api_hash`，请在 https://my.telegram.org/apps 获取；
* Bot `token`，请与 [@BotFather](https://t.me/BotFather) 聊天获取。

### 3. 创建配置文件和数据库
#### 创建配置文件
配置文件路径 `~/.config/tgficbot.cfg`
创建
```sh
@ cd ~ && clear
@ mkdir .config && cd .config
@ vi tgficbot.cfg
```
配置文件格式如下：
```
ini
[api]
id = 123456
hash = xxxxxxxxxxxxxxxxx

[bot]
token = 123456789:xxxxxxxxxxxxxxxxxxxx
```

#### 创建数据库
运行时的数据库将被放在 `~/.cache/tgficbot.db`。
```sh
@ cd ~ && clear
@ mkdir .cache && cd .cache
# 创建一个空的数据库，然后保存
@ sqlite3 tgficbot.db
> .quit
```
### 4. 安装
克隆/下载这个仓库，然后安装：
这里将项目安装到 `/home`

```sh
cd /home
git clone https://github.com/jsmjsm/telegram-find-in-channel-bot.git
cd telegram-find-in-channel-bot
python3 setup.py install
```

（可选）安装 `cryptg` 可提速：

```sh
apt update
apt install clang python3-dev
pip3 install -U --user cryptg
```
### 5. 启动&后台持续运行：
这里用了 `nohup` 和 `&` 使bot能在不关机的前提下持续运转
```sh
cd /home/telegram-find-in-channel-bot
nohup python3 -m tgficbot.main > find_bot.log3 2>&1 &
```
通过 `ps -a `可以看到 python在后台运行， 可以用 `kill` 杀死 bot

## 使用
需要先将Bot加入你想搜索的频道，并设置成频道管理员
按照 Bot 的操作提示建立搜索库（内容多的频道需要耗费超长时间）
/find 开始搜索会话

----
Here is the English RAW Deploy manual
without any edition

## Deploy

Instead of HTTP bot API, this bot uses MTProto client API. Please obtain these tokens:

* App `api_id` and `api_hash`, please obtain it at https://my.telegram.org/apps;
* Bot token, please obtain it by talking to [@BotFather](https://t.me/BotFather).

Clone this repo and install:

```sh
cd telegram-find-in-channel-bot
python3 setup.py install
```

(Optional) If `cryptg` is installed, the bot will work faster:

```sh
apt update
apt install clang python3-dev
pip3 install -U --user cryptg
```

Configuration file is `~/.config/tgficbot.cfg`, here's the format:

```ini
[api]
id = 123456
hash = xxxxxxxxxxxxxxxxx

[bot]
token = 123456789:xxxxxxxxxxxxxxxxxxxx
```

To run:

```sh
python3 -m tgficbot.main
```

The database will be placed at `~/.cahce/tgficbot`.
