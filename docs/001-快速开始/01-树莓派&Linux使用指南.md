# 树莓派接入
`本文档适用于树莓派及其他Linux设备`  

## 连接硬件
将aily shell zero连接到树莓派  
> aily shell zero 支持树莓派Zero、4B、5B及其他遵循树莓派引脚定义的Linux开发板  

（图片待做）

## 安装&运行  
确保树莓派已经联网（可以接网线或连接wifi），终端中运行以下指令安装aily sdk：
```bash
pip install aily-py
```
## 使用准备  
aily的运行依赖大模型API，理论上遵循OpenAI接口标准的主流模型，均可使用。
使用aily前，请先通过以下链接获取到模型API key  
[OpenAI GPT key获取](https://platform.openai.com/api-keys)  
[ZhiPu GLM key获取(中国大陆推荐)](https://open.bigmodel.cn/usercenter/apikeys)  

## 基础配置
以下三种方法任选其一进行基础配置  
### 方法1：通过app配置
0. 启动aily服务
```bash
aily-cli run  
```  
1. 安装aily Config Tool App  
[android下载]()  [IOS下载]()    

2. 通过app选择模型并填入key  
在App中选择使用的模型，并填入key

### 方法2：运行时填入配置  
创建项目及配置文件
```bash
aily-cli run --model gpt-4o --key <xxxxxxxxxxx>
```

### 方法3：通过.env文件配置
```bash
aily-cli new aily-test
cd aily-test
echo "MODEL=gpt-4o\n KEY=xxxxxxxx" | cat - >> .env 
aily-cli run
```
你可以通过修改.env文件，修改相关配置
[阅读了解更多.env配置]()  

## 运行测试  
通过默认唤醒词“你好，艾莉”，唤醒设备，然后对话吧。

## 更多
· [使用Python进行开发]()  
· [进行配置工具进行配置]()  
· [.env可用配置项说明]()  
. [aily Shield数据手册]()
