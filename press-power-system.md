# 隆源压滤机液压站、油缸与电机参数数据库

本文件记录公司标准机型的动力系统配置（液压站选型、油缸对照及全机电机参数），用于外贸报价单（Quotation）电气与液压参数的快速填充。

---

## ⚗️ 1. 液压系统与油缸核心规范（Hydraulic & Cylinder Specs）

压滤机的自动保压和拉板动作全靠液压驱动。根据公司标准，液压核心参数必须严格执行以下标定：

### [cite_start]A. 液压站核心工作压力（Hydraulic Station Pressure） [cite: 142]
* [cite_start]**额定标定上限压力**：**25 MPa** [cite: 183, 198] [cite_start]—— 当油压上升到电接点压力表上限值时，主油泵自动关停，压滤机进入自动保压状态 [cite: 142, 183]。
* [cite_start]**安全溢流阀锁定压力**：**29 MPa** [cite: 164, 241] [cite_start]—— 出厂前已锁死，用于极限超压保护，严禁用户和业务员私自建议调整 [cite: 164, 241]。
* [cite_start]**常规液压油箱容积**：初次加注大约 **65 L** 清洁液压油 [cite: 163]。
* [cite_start]**外贸换油提示**：新机在使用 1-2 周后需更换液压油，第二次周期为一个月的空载运行循环清洗，后续每 6 个月左右更换一次 [cite: 248]。

### [cite_start]B. 油缸结构与滑动底座（Cylinder & Sliding Foot） [cite: 296, 297]
* [cite_start]**结构类型**：标准焊接式高压油缸总成 (Welded High-Pressure Hydraulic Cylinder) [cite: 304]。
* **纵向滑动位移设计（外贸技术澄清核心点）**：
  * [cite_start]进料端（止推板端）在基础上是完全固定的 [cite: 77]。
  * [cite_start]**压紧端（油缸座端）严禁固定！** [cite: 77] [cite_start]压滤机安装到位后，必须拆除油缸座与其下支脚之间的联接螺栓 [cite: 96]。
  * [cite_start]允许油缸座与下支脚之间进行轴向的纵向位移滑动，以吸收设备工作受力状态下的热胀冷缩和主梁主轴向应力，防止主梁弯曲变形 [cite: 77, 96, 150]。

---

## [cite_start]⚡ 2. 压滤机全机电机与电气参数标准（Motor & Electrical Specs） [cite: 125]

外国客户（尤其是欧美、中东）的工业电网电压和频率各不相同（如 380V/50Hz, 415V/50Hz, 460V/60Hz 等）。在做技术合规时，必须向客户明示以下三个核心电机的标定参数：

### [cite_start]A. 主液压油泵电机 (Main Hydraulic Pump Motor) [cite: 142, 299]
* [cite_start]**核心功能**：驱动高压柱塞泵，提供滤板压紧所需的液压动力 [cite: 142]。
* **外贸标准报价参数**：
  * [cite_start]标准功率：通常为 **4 kW**（需根据 1000型/1250型具体面积核对对应的柱塞泵排量） [cite: 313]。
  * [cite_start]控制特性：配合电接点压力表实现自动启停保压（压力降至下限时自动启动上压） [cite: 142]。

### [cite_start]B. 自动拉板电机 / 液压马达 (Automatic Plate Shifter Motor) [cite: 136, 296, 297]
* [cite_start]**核心功能**：驱动传动链条，带动机械手自动逐块拉开滤板进行卸料 [cite: 136]。
* [cite_start]**控制特性**：机械手的自动换向和保护靠**变频器（Inverter）**通过电流大小切换或时间继电器控制 [cite: 136]。外贸报价时如果客户要全自动机型，必须注明带“变频控制拉板小车 (VFD Controlled Plate Shifter)”。

### [cite_start]C. 辅助配套电机参数 (Auxiliary Motors) [cite: 125, 286]
* [cite_start]**进料泵电机 (Feed Pump Motor)**：由买方自备或我司配套，其功率和流量必须与我司压滤机最大设计过滤压力相匹配（泵的压力绝对不允许超过设备最大过滤压力） [cite: 152, 156]。

---

## 📋 3. 动力系统外贸报价单描述模板（英文）

当你在写正式的英语报价单时，可以直接将以下技术参数模块（Technical Specification Block）复制进你的邮件或 Excel 报价单中：

```text
============================================================
TECHNICAL SPECIFICATION - POWER & HYDRAULIC SYSTEM
============================================================
1. Hydraulic System:
   - Rated Squeezing Pressure: 25 MPa (Automatic Pressure Maintenance)
   - Max. Safety Valve Pressure: 29 MPa (Factory Locked)
   - Cylinder Type: High-strength Welded Hydraulic Cylinder
   - Structural Feature: Sliding cylinder seat design to prevent main beam deformation under stress.

2. Electrical & Motor Specifications:
   - Main Hydraulic Motor Power: 4.0 kW 
   - Plate Shifting Drive: VFD (Variable Frequency Drive) Automatic Shifter
   - Standard Voltage Option: 380V-415V/50Hz/3Phase (Customizable per request)
   - Control Cabinet: Centralized PLC Control System with Emergency Stop Button
============================================================
