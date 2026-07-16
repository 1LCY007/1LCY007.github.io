# RepoFlow

![image-20260716152046597](C:\Users\luochunyang\AppData\Roaming\Typora\typora-user-images\image-20260716152046597.png)

## TaskBoard 演示案例

**左侧是我们的**B001的任务演示视频，

**实验条件：完善****prompt+完全无记忆初始化。

* 观察分析：有board的初始化时间（上）和无board的版本（下）几乎一致，说明初始化效率几乎不影响

**右侧是我们的**B002的任务演示视频，

**实验条件：完善**prompt+基于B001对应项目文件+无记忆
**观察分析：我们**B002完成速度明显区分开，无board的版本时间是有board版本的两倍。

## RepoAdaptive自规划

**测试对象：3个在github上开源的项目**

**测试方法：用health_review对代码健康度进行检测，主要测试skill在大工程项目下的性能**

**使用模型：kimi-2.7-code**

**[1. ](https://github.com/fastapi/full-stack-fastapi-template?utm_source=chatgpt.com)**[fastapi/full-stack-fastapi-template: Full stack, modern web application template. Using FastAPI, React, SQLModel, PostgreSQL, Docker, GitHub Actions, automatic HTTPS and more.](https://github.com/fastapi/full-stack-fastapi-template?utm_source=chatgpt.com)

**[2. ](https://github.com/open-webui/open-webui?utm_source=chatgpt.com)**[open-webui/open-webui: User-friendly AI Interface (Supports Ollama, OpenAI API, ...)](https://github.com/open-webui/open-webui?utm_source=chatgpt.com)

**[3. ](https://github.com/apache/superset?utm_source=chatgpt.com)**[apache/superset: Apache Superset is a Data Visualization and Data Exploration Platform](https://github.com/apache/superset?utm_source=chatgpt.com)

### **检查结果比较**——Token层面

![e31fedf35c7da54fcd896987e51fbc12](G:\xwechat_files\wxid_u2fhd1k77i8121_1dfc\temp\RWTemp\2026-07\9e20f478899dc29eb19741386f9343c8\e31fedf35c7da54fcd896987e51fbc12.png)

### 检查结果比较--对比重点层面

![image-20260716152012121](C:\Users\luochunyang\AppData\Roaming\Typora\typora-user-images\image-20260716152012121.png)