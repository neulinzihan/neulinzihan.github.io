3/1/2026

---

**index.html（主页）**

- 每个项目卡片加了 `.project-pitch` 电梯pitch行，左侧accent竖线
- Resume CTA 从四选一下拉改为：主按钮直接链接Full Resume，旁边小箭头展开其他版本
- Hero区动效放慢（delay拉大，scroll-hint透明度降低）
- 移动端新增固定chapter nav条（Projects / Experience / Education / Inspiration）
- 三个项目图片替换为更相关的Unsplash图
- 主题切换写入sessionStorage，供子页面继承
- 7个次要项目移出主页，改为"View more projects →"按钮链接到独立页面

---

**projects-more.html（新建）**

- 包含7个次要项目：Robotic Arm、Drone Sim、Vehicle Control、FEA、Flow Sensor、Sleep Study、Spaghetti Bridge
- 顶部固定chapter nav，滚动自动高亮对应项目
- 每个card默认只显示pitch，点"Details"展开详细描述
- 左下角sticky"← Main projects"按钮，滚动300px后浮现
- 底部保留原有大号back按钮
- sessionStorage主题继承

---

**resume.html**

- 三个tab（Full / Test Engineer / R&D）保留，视觉优化
- 每个工作/项目entry改为可折叠：默认显示职位+单位+一行JetBrains Mono的pitch，点"+"展开bullet points
- Education、Skills用 `.section-group` 浅色背景区隔，section间呼吸感更强
- Skills改为stripe行布局，字体层级加大对比度
- sessionStorage主题继承，同时保留`?theme=`URL参数兜底

---

**toolbox.html**

- Proficient pills加hover tooltip，显示"在哪个具体项目里用过"（例如SolidWorks → "Indenters, compliant linkage, test fixtures, PCBA enclosures"）
- 加了提示文字"Hover over any pill to see where it was used"
- sessionStorage主题继承

---

**courses.html**

- 每个card加`::before`伪元素，hover时顶部出现2px accent色bar
- hover同时有`translateY(-4px)` + shadow，层次感更强
- sessionStorage主题继承

---

**about-me.html**

- 从纯文字墙改为Apple image accordion结构
- 7个section全部做成可折叠卡片（what drives me / hands-on / how I learn / beyond engineering / product ideas / what I watch / a few more things）
- 默认展开第一个，其余收起
- 每个section有emoji icon + 标题 + "+"按钮
- 结尾引言改为带左侧accent border的卡片样式
- sessionStorage主题继承

---

**所有页面共同改动**

- 统一使用sessionStorage传递主题色，从主页切换主题后跳转到任何子页面不会出现颜色跳变
- toolbox和courses同时保留`?theme=`URL参数作为兜底，兼容直接链接访问