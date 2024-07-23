# aily cli
aily cli是本项目提供的命令行工具，可用于启动项目、管理配置、查看日志。


## 项目启动
```
aily-cli run
```
### 带参数启动
```
aily-cli run  --model gpt-4o --key sk-xxxxxxxxx
```

### 输出使用日志


## 可用配置项
```
LLM_URL=''  // 大模型接口地址
LLM_KEY=''  // 大模型服务Key
LLM_MODEL_NAME='' // 模型名称
LLM_TEMPERATURE='' // 模型温度设置
LLM_PRE_PROMPT=''  // 提示词

# 使用语音转文字工具(speech_to_text_by_sr)时需要填写微软azure语音服务的key
AZURE_KEY=''
```

## 日志查看  
