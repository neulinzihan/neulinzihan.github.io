# 个人化AI助手完整架构设计

## 项目概述
一个完全本地化、以圣经三观为基础的个人AI助手系统。所有数据加密存储在本地设备上，具备通讯、信息管理、问题解决能力。

---

## 第一部分：技术栈选择

### 后端框架
- **语言**：Python 3.10+
- **主框架**：FastAPI（轻量、高效、支持异步）
- **数据库**：SQLite + SQLAlchemy ORM（本地存储）
- **加密**：cryptography库（AES-256加密敏感数据）
- **任务队列**：APScheduler（定时任务）

### 前端
- **UI框架**：Streamlit（快速原型）或 Vue.js（更强大）
- **通讯交互**：WebSocket实时通讯

### AI集成
- **主模型**：Claude API（通过本地调用，API密钥本地加密存储）
- **离线功能**：ollama（支持本地开源模型如Llama作为备选）

### 通讯集成
- **短信**：twilio-python（需付费，但隐私有保障）/ 或 运营商API
- **邮件**：smtplib + imaplib（本地收发，Gmail/企业邮箱）
- **微信**：itchat或WeChat官方Bot API
- **电话**：twilio-python Voice API

### 部署环境
- **本地运行**：Windows/Mac/Linux PC 或 Raspberry Pi
- **容器化**：Docker（可选，便于迁移）
- **系统服务**：设置为后台服务（systemd on Linux / Task Scheduler on Windows）

---

## 第二部分：系统架构

```
┌─────────────────────────────────────────────┐
│         前端界面 (Streamlit/Vue)            │
│    用户交互 · 信息展示 · 设置管理           │
└────────────────┬────────────────────────────┘
                 │
┌────────────────▼────────────────────────────┐
│        API层 (FastAPI)                      │
│   • 请求路由 · 认证 · 日志记录              │
└────────────────┬────────────────────────────┘
                 │
    ┌────────────┼────────────┬─────────────┐
    │            │            │             │
┌───▼───┐  ┌─────▼──┐  ┌─────▼────┐  ┌────▼────┐
│ 记忆  │  │ AI推理 │  │  任务执行 │  │  数据库  │
│ 系统  │  │ 引擎   │  │  引擎     │  │  系统    │
└───┬───┘  └─────┬──┘  └─────┬────┘  └────┬────┘
    │            │           │            │
    │  ┌─────────▼───────┐   │            │
    └──►│ Claude API调用  │   │   ┌────────┴──────────┐
       │ (本地加密密钥)  │   │   │ SQLite + 加密存储 │
       └─────────────────┘   │   └──────────┬────────┘
                             │             │
              ┌──────────────┼─────────────┤
              │              │             │
        ┌─────▼────┐  ┌─────▼──┐  ┌──────▼──┐
        │ 微信集成 │  │ 邮件   │  │ 短信/电话│
        │ itchat   │  │SMTP   │  │ Twilio  │
        └──────────┘  └────────┘  └─────────┘
```

---

## 第三部分：核心功能模块设计

### 1. 记忆与个人资料管理 (Memory Module)

```python
# 核心数据结构
class PersonalProfile:
    - name: 姓名
    - birth_date: 出生日期
    - faith_background: 信仰背景（圣经学习进度、教义偏好）
    - work_style: 工作风格（协作方式、偏好工具）
    - daily_habits: 日常习惯（作息、运动、爱好）
    - communication_style: 沟通风格（偏好语言、表达方式）
    - important_dates: 重要日期（生日、纪念日）
    - relationships: 关系网络（家人、朋友、同事）

class MemoryEntry:
    - timestamp: 记录时间
    - category: 分类（工作/生活/学习/信仰）
    - content: 内容
    - context: 上下文
    - relevance_score: 相关性评分
    - encrypted: 加密标记
```

**实现方式**：
- 每次对话后自动提取关键信息，存储到本地数据库
- 使用向量嵌入（embedding）为记忆建立语义索引
- 查询时智能检索最相关的记忆片段注入到Claude上下文

### 2. AI推理引擎 (Reasoning Engine)

```python
class AIAssistant:
    def __init__(self):
        self.system_prompt = self._build_system_prompt()
        self.memory_manager = MemoryManager()
        self.values_checker = BibleValuesChecker()
    
    def _build_system_prompt(self):
        """
        核心系统提示，融合：
        1. 个人背景和三观
        2. 圣经伦理框架
        3. 沟通风格偏好
        4. 隐私和安全原则
        """
        return f"""
        你是{user_name}的个人AI助手。
        
        【个人背景】
        {personal_profile}
        
        【信仰原则】
        你以圣经真理为基础提供建议。具体包括：
        - 爱邻舍如己的伦理
        - 诚实、正直的价值观
        - 对生命、家庭、社区的尊重
        - 属灵成长的关注
        
        【工作风格】
        {work_style_preferences}
        
        你的回答应该：
        1. 考虑使用者的具体情况和背景
        2. 引用圣经原则当涉及道德问题时
        3. 尊重使用者的隐私，不主动提及个人信息
        4. 若发现问题超出你的能力，诚实地说明
        """
    
    async def process_query(self, user_message: str):
        # 1. 检索相关记忆
        relevant_memories = self.memory_manager.retrieve(user_message)
        
        # 2. 构建完整上下文
        context = self._build_context(relevant_memories)
        
        # 3. 价值观检查（圣经原则）
        is_aligned = self.values_checker.validate(user_message)
        
        # 4. 调用Claude
        response = await self._call_claude_api(
            messages=[
                {"role": "system", "content": self.system_prompt},
                {"role": "user", "content": f"{context}\n\n用户问题：{user_message}"}
            ]
        )
        
        # 5. 保存交互记录
        self.memory_manager.save(user_message, response)
        
        return response
```

### 3. 任务执行引擎 (Task Execution Engine)

```python
class TaskExecutor:
    """处理具体的操作任务"""
    
    async def send_message(self, platform: str, recipient: str, content: str):
        """发送消息（短信/邮件/微信）"""
        if platform == "sms":
            return await self.twilio_client.send_sms(recipient, content)
        elif platform == "email":
            return await self.email_service.send(recipient, content)
        elif platform == "wechat":
            return await self.wechat_client.send_message(recipient, content)
    
    async def make_call(self, phone_number: str):
        """拨打电话"""
        return await self.twilio_client.make_call(phone_number)
    
    async def schedule_task(self, task_description: str, datetime_str: str):
        """计划任务"""
        # 使用APScheduler
        scheduled_task = self.parser.parse_task(task_description)
        self.scheduler.add_job(
            scheduled_task['action'],
            'cron',
            **scheduled_task['schedule_params']
        )
```

### 4. 加密数据管理 (Encryption Module)

```python
from cryptography.fernet import Fernet
from cryptography.hazmat.primitives import hashes
from cryptography.hazmat.primitives.kdf.pbkdf2 import PBKDF2

class SecureStorage:
    def __init__(self, master_password: str):
        # 从主密码推导密钥
        salt = b'your_app_salt'  # 或从本地文件读取
        kdf = PBKDF2(
            algorithm=hashes.SHA256(),
            length=32,
            salt=salt,
            iterations=100000,
        )
        key = base64.urlsafe_b64encode(kdf.derive(master_password.encode()))
        self.cipher = Fernet(key)
    
    def encrypt_data(self, data: str) -> str:
        """加密数据"""
        return self.cipher.encrypt(data.encode()).decode()
    
    def decrypt_data(self, encrypted_data: str) -> str:
        """解密数据"""
        return self.cipher.decrypt(encrypted_data.encode()).decode()
    
    def store_sensitive(self, key: str, value: str):
        """存储敏感数据（如API密钥）"""
        encrypted = self.encrypt_data(value)
        db.save(key, encrypted)
    
    def retrieve_sensitive(self, key: str) -> str:
        """读取敏感数据"""
        encrypted = db.load(key)
        return self.decrypt_data(encrypted)
```

### 5. 圣经价值观检查器 (Bible Values Checker)

```python
class BibleValuesChecker:
    """确保AI的建议符合圣经原则"""
    
    def __init__(self):
        self.bible_principles = {
            "love": "爱是律法的总和（罗13:8-10）",
            "honesty": "说谎言是神所恨恶的（箴6:16-19）",
            "forgiveness": "饶恕如同主饶恕你（弗4:32）",
            "patience": "要存忍耐心（林前13:4）",
            "justice": "申冤在我，我必报应（罗12:19）",
        }
    
    def validate(self, query: str, response: str) -> bool:
        """检查回答是否符合圣经原则"""
        # 使用NLP分析回答中的价值倾向
        # 对照圣经原则数据库
        # 返回是否通过检查
        
        red_flags = [
            "鼓励报复",
            "贪婪",
            "不诚实",
            "伤害他人",
        ]
        
        for flag in red_flags:
            if flag in response:
                return False
        return True
    
    def enrich_response(self, response: str, topic: str) -> str:
        """如果相关，添加圣经智慧"""
        if topic in self.bible_principles:
            response += f"\n\n【圣经智慧】{self.bible_principles[topic]}"
        return response
```

---

## 第四部分：数据库设计

### SQLite Schema

```sql
-- 用户资料表
CREATE TABLE user_profile (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    birth_date DATE,
    faith_background TEXT,
    work_style TEXT,
    daily_habits TEXT,
    encrypted BOOLEAN DEFAULT 1
);

-- 记忆表
CREATE TABLE memories (
    id INTEGER PRIMARY KEY,
    user_id INTEGER,
    category TEXT,
    content TEXT,
    timestamp DATETIME DEFAULT CURRENT_TIMESTAMP,
    context TEXT,
    relevance_score FLOAT,
    embedding BLOB,
    encrypted BOOLEAN DEFAULT 1
);

-- 通讯记录表
CREATE TABLE communications (
    id INTEGER PRIMARY KEY,
    type TEXT,  -- sms, email, wechat, call
    recipient TEXT,
    content TEXT,
    timestamp DATETIME,
    status TEXT,
    encrypted BOOLEAN DEFAULT 1
);

-- API密钥表（加密存储）
CREATE TABLE api_keys (
    id INTEGER PRIMARY KEY,
    service TEXT,
    key_encrypted BLOB,
    created_at DATETIME
);

-- 交互日志表
CREATE TABLE interaction_logs (
    id INTEGER PRIMARY KEY,
    user_message TEXT,
    ai_response TEXT,
    timestamp DATETIME,
    metadata TEXT
);
```

---

## 第五部分：实施步骤

### Phase 1: 核心框架（2-3周）
- [ ] 搭建FastAPI后端基础
- [ ] 配置SQLite数据库和加密系统
- [ ] 实现Claude API集成
- [ ] 构建基础Streamlit前端

### Phase 2: 记忆系统（2周）
- [ ] 实现个人资料管理模块
- [ ] 开发记忆提取和索引系统
- [ ] 建立向量嵌入（可用OpenAI embeddings）

### Phase 3: 通讯集成（2-3周）
- [ ] 集成邮件功能（SMTP/IMAP）
- [ ] 集成微信API或itchat
- [ ] 集成Twilio（短信和电话）
- [ ] 测试各通讯渠道

### Phase 4: 特殊功能（2周）
- [ ] 开发圣经价值观检查器
- [ ] 实现计划任务系统（APScheduler）
- [ ] 完善错误处理和日志

### Phase 5: 安全和部署（1-2周）
- [ ] 完整的密钥管理系统
- [ ] 本地备份和恢复机制
- [ ] Docker容器化
- [ ] 系统服务配置

---

## 第六部分：关键代码示例

### 项目结构

```
personal-ai-assistant/
├── backend/
│   ├── app.py                 # FastAPI主应用
│   ├── config.py              # 配置管理
│   ├── models/
│   │   ├── user.py
│   │   ├── memory.py
│   │   └── communication.py
│   ├── services/
│   │   ├── ai_service.py
│   │   ├── memory_service.py
│   │   ├── encryption_service.py
│   │   ├── communication_service.py
│   │   └── task_executor.py
│   ├── core/
│   │   ├── security.py
│   │   ├── bible_values.py
│   │   └── logger.py
│   └── requirements.txt
├── frontend/
│   ├── app.py                 # Streamlit应用
│   ├── pages/
│   │   ├── chat.py
│   │   ├── memory.py
│   │   ├── settings.py
│   │   └── communications.py
│   └── utils.py
├── database/
│   └── schema.sql
├── docker-compose.yml
└── README.md
```

### 最小化启动脚本 (app.py)

```python
from fastapi import FastAPI, WebSocket
from fastapi.cors.middleware import CORSMiddleware
import uvicorn
from services.ai_service import AIAssistant
from services.encryption_service import SecureStorage
from core.logger import setup_logger

logger = setup_logger(__name__)

app = FastAPI(title="个人AI助手")

# 跨域配置（本地访问）
app.add_middleware(
    CORSMiddleware,
    allow_origins=["localhost", "127.0.0.1"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

# 全局初始化
secure_storage = None
ai_assistant = None

@app.on_event("startup")
async def startup_event():
    global secure_storage, ai_assistant
    
    # 初始化加密存储
    master_password = input("请输入主密码以启动助手: ")
    secure_storage = SecureStorage(master_password)
    
    # 初始化AI助手
    ai_assistant = AIAssistant(secure_storage)
    logger.info("助手已启动")

@app.post("/api/chat")
async def chat(message: str):
    """处理用户消息"""
    response = await ai_assistant.process_query(message)
    return {"response": response}

@app.post("/api/send-message")
async def send_message(platform: str, recipient: str, content: str):
    """发送消息"""
    result = await ai_assistant.task_executor.send_message(
        platform, recipient, content
    )
    return {"status": "success", "result": result}

@app.get("/api/memory")
async def get_memories(limit: int = 10):
    """获取最近的记忆"""
    memories = ai_assistant.memory_manager.get_recent(limit)
    return {"memories": memories}

if __name__ == "__main__":
    uvicorn.run(
        app,
        host="127.0.0.1",
        port=8000,
        log_level="info"
    )
```

---

## 第七部分：安全建议

1. **主密码管理**
   - 使用强密码（16+ 字符）
   - 定期更改
   - 不要与他人共享

2. **API密钥安全**
   - 所有密钥使用AES-256加密存储
   - 不要在代码中硬编码
   - 定期轮换（尤其是Twilio密钥）

3. **数据备份**
   - 定期加密备份到外部存储
   - 使用物理隔离的备份介质（USB、硬盘）
   - 测试恢复流程

4. **网络安全**
   - 仅在本地网络运行（127.0.0.1）
   - 如需远程访问，使用VPN（WireGuard）
   - HTTPS使用自签名证书

5. **日志安全**
   - 不记录敏感信息（密钥、密码）
   - 定期清理日志
   - 加密日志文件

---

## 第八部分：成本估算

| 服务 | 用途 | 月成本 | 备注 |
|------|------|--------|------|
| Claude API | AI推理 | $3-15 | 按usage付费 |
| Twilio | 短信/电话 | $1-5 | 按需付费 |
| 微信Bot | 消息接收 | 免费 | 个人用免费 |
| 邮件服务 | SMTP | 免费 | 使用现有邮箱 |
| **总计** | | **$4-20** | 可完全本地部署 |

---

## 第九部分：常见问题

**Q: 如何保证完全离线？**
A: 仅在涉及Claude API调用时需要网络。可选使用ollama搭建本地LLM服务。

**Q: 如何处理记忆的遗忘？**
A: 使用向量相似度和LRU缓存策略，定期优化索引。

**Q: 如何修改圣经价值观检查器？**
A: 在`bible_values.py`中编辑原则列表，可根据个人学习不断完善。

**Q: 数据泄露风险？**
A: 完全本地存储+AES-256加密大幅降低风险。定期审计代码和依赖库。

---

## 下一步建议

1. **克隆/创建项目仓库**：使用git管理版本
2. **开发环境搭建**：Python虚拟环境 + 必要依赖
3. **先从MVP开始**：简单的聊天 + 记忆 + 一种通讯方式
4. **逐步扩展**：添加更多功能和集成
5. **定期测试和优化**：特别是隐私和安全方面