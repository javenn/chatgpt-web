# chatgpt-web
[![Release](https://img.shields.io/github/v/release/869413421/chatgpt.svg?style=flat-square)](https://github.com/869413421/wechatbot/releases/tag/v1.1.3)
![Github stars](https://img.shields.io/github/stars/869413421/chatgpt.svg)
![Forks](https://img.shields.io/github/forks/869413421/chatgpt.svg?style=flat-square)
> 本项目可以一键部署属于自己定制化的 chatgpt web程序，
> 只需下载release中对应平台的项目文件，修改配置后执行，打开 http://127.0.0.1:8080 ，便可以获得属于自己的chatgpt网站。
> 
> 参考项目：[codegen](https://github.com/git-cloner/codegen)

> 项目当前默认为示例中AI聊天机器人参数，可以根据自己需求定制化。
> 
> **注意，每个参数都可能影响你得到不一样的聊天效果,改变一个参数你就可能得到另一种回答，所以请自己尝试去调试，不要上来就抱怨人工智障。文档中有二十多中参数示例，如AI聊天机器人
> ，产品名称生成，python代码修复器等等等...**
> 
> 详情参考官方详细[参数示例](https://beta.openai.com/examples)

# 项目初衷
> 自chatgpt流行以后，一直在使用其作为自己的编码工具。奈何官网时常在问题问到一半时短路，一些得到的答案就此丢失。
> 为了解决这个问题，我选择了更加稳定的API套上客户端来作为自己的工具。定制化地做了一些功能，如存储提问记录，统计提问信息等一些功能，同时做上内网穿透提供给没有办法体验chatgpt的朋友使用，由此大大降低了使用门槛。
> 当前项目是初始功能版本，开源出来给有需要的朋友使用。

# 项目功能
* 基本问答界面
* 机器人参数可配置

# 使用前提
> 有openai账号，并且创建好api_key，注册事项可以参考[此文章](https://juejin.cn/post/7173447848292253704) 。

# 快速开始

`第一种：直接下载二进制(适合对编程不了解的同学)`

> 非技术人员请直接下载release中的[压缩包](https://github.com/869413421/wechatbot/releases) ，请根据自己系统以及架构选择合适的压缩包，下载之后直接解压运行。

下载之后，在本地解压，即可看到可执行程序，与配置文件：

```
# windows
1.下载压缩包解压
2.复制文件中config.dev.json更改为config.json
3.将config.json中的api_key替换为自己的
4.双击exe运行，启动服务

# linux
$ tar xf chatgpt-web-v0.0.2-darwin-arm64.tar.gz # 解压
$ cd chatgpt-web-v0.0.2-darwin-arm64
$ cp config.dev.json # 根据情况调整配置文件内容
$ ./chatgpt-web  # 直接运行

# 如果要守护在后台运行
$ nohup ./chatgpt-web &> run.log &
$ tail -f run.log
```

`第二种：基于源码运行(适合了解go语言编程的同学)`

````
# 获取项目
$ git clone https://github.com/869413421/chatgpt-web.git

# 进入项目目录
$ cd chatgpt-web

# 复制配置文件
$ copy config.dev.json config.json

# 启动项目
$ go run main.go
````

# 使用docker运行
你可以使用docker快速运行本项目。
`第一种：基于环境变量运行`

```sh
# 运行项目，环境变量参考下方配置说明
$ docker run -itd --name chatgpt-web --restart=always \
 -e APIKEY=换成你的key \
 -e MODEL=text-davinci-003 \
 -e MAX_TOKENS=512 \
 -e TEMPREATURE=0.9 \
 -e TOP_P=1 \
 -e FREQ=0.0 \
 -e PRES=0.6 \
 -p 8080:8080 \
 docker.mirrors.sjtug.sjtu.edu.cn/qingshui869413421/chatgpt-web:latest
```

运行命令中映射的配置文件参考下边的配置文件说明。

`第二种：基于配置文件挂载运行`

```sh
# 复制配置文件，根据自己实际情况，调整配置里的内容
$ cp config.dev.json config.json  # 其中 config.dev.json 从项目的根目录获取

# 运行项目
$ docker run -itd --name chatgpt-web -v `pwd`/config.json:/app/config.json -p 8080:8080 docker.mirrors.sjtug.sjtu.edu.cn/qingshui869413421/chatgpt-web:latest
```

其中配置文件参考下边的配置文件说明。



# 配置文件说明

````
{
  "api_key": "your api key",
  "port": 8080,
  "bot_desc": "以下是与AI助手的对话。助手乐于助人，富有创造力，聪明且非常友好。",
  "max_tokens": 512,
  "model": "text-davinci-003",
  "temperature": 0.9,
  "top_p": 1,
  "frequency_penalty": 0.0,
  "presence_penalty": 0.6
}

api_key：openai api_key
port: http服务端口
bot_desc：AI特征，非常重要，功能等同给与AI一个身份设定
max_tokens: GPT响应字符数，最大2048，默认值512。max_tokens会影响接口响应速度，字符越大响应越慢。
model: GPT选用模型，默认text-davinci-003，具体选项参考官网训练场
temperature: GPT热度，0到1，默认0.9。数字越大创造力越强，但更偏离训练事实，越低越接近训练事实
top_p: 使用温度采样的替代方法称为核心采样，其中模型考虑具有top_p概率质量的令牌的结果。因此，0.1 意味着只考虑包含前 10% 概率质量的代币。
frequency_penalty: 
presence_penalty:
````
### 有疑问请添加微信（备注: chatgpt-web），不定期通过解答

**微信号 huangyanming681925**