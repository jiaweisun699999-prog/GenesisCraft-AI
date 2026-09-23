# 🌍 GenesisCraft-AI

<div align="center">

> **从单体具身智能到沙盒文明演化**  
> *Empowering autonomous LLM‑driven agents to perceive, collaborate, and evolve civilizations inside Minecraft.*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Node.js 18+](https://img.shields.io/badge/Node.js-18%2B-green.svg)](https://nodejs.org/)
[![Minecraft 1.20+](https://img.shields.io/badge/Minecraft-1.20%2B-red.svg)](https://www.minecraft.net/)

[核心特性](#-核心特性) • [系统架构](#-系统架构) • [快速开始](#-快速开始) • [项目路线图](#-项目路线图-roadmap) • [贡献指南](#-贡献指南)

</div>

---

## 📖 项目简介

**GenesisCraft‑AI** 是一个面向 Minecraft 的自主具身智能与多智能体文明演化框架。项目突破了传统命令行 RCON 机器人的无实体限制，通过双层解耦架构（Python 认知决策 + Node.js 物理具身），为智能体赋予了独立视线感知、物理碰撞、复杂寻路与自愈执行能力。

从最初作为贴身探险、挖矿建造的**全能陪玩伙伴**，逐步演进为具有长期记忆流、社会分工与自由贸易机制的**沙盒文明模拟世界**。

---

## ✨ 核心特性

- 🤖 **真实具身物理实体 (Embodied Entity):** 基于 Headless Client 协议，拥有真实碰撞箱、血量与饥饿度，支持视线对视（Raycasting）与真实手部交互。
- 🧠 **端云协同分层决策:** 底层行为树与 Baritone 处理毫秒级寻路避障（0 Token 消耗）；高阶社交、任务规划与反思按需唤醒大模型（降低 75%+ Token 成本）。
- 🛠️ **闭环自愈机制 (Action Critic):** 遇到地形受阻、合成材料不足或环境怪物突袭时，自动捕获环境反馈并回传大模型修正重试，保障复杂长链路任务的成功率。
- 🏛️ **群体文明演化 (Civilization Simulation):** 结合 *Generative Agents* 记忆流架构，支持多 NPC 记忆沉淀、好感度系统、职业分工、集市贸易与聚落共建。

---

## 🏗️ 系统架构

```mermaid
flowchart TD
    subgraph Top["顶层大脑 - 认知与社会学模拟"]
        lang["Python (FastAPI / LangGraph / Redis)"]
        subgraph Agents
            A["单体陪玩 Agent<br/>• 短期对话上下文<br/>• 工具链决策 (Function Calling)<br/>• Action Critic (容错反思自愈)"]
            B["群体文明演化调度<br/>• 长期记忆流与反思 (Generative Agents)<br/>• 领地网格与以物易物交易总线<br/>• 事件广播 (Event Broker)"]
        end
    end

    RPC["跨语言 RPC 通信协议 (WebSocket)"]

    subgraph Bottom["底层小脑 - 具身驱动与空间控制"]
        node["Node.js (Mineflayer + Baritone)"]
        impl["• 视线射线检测 (Raycasting)<br/>• 复杂地形 A* 寻路与避障<br/>• 方块放置 / 挖掘 / 物品合成 / 背包同步"]
    end

    mc["Minecraft Server (Paper / Docker)"]

    Top --> RPC
    A --> RPC
    B --> RPC
    RPC --> Bottom
    node --> impl
    Bottom --> mc

    lang --> A
    lang --> B

    classDef topStyle fill:#253b56,stroke:#4285d4,color:#fff
    classDef rpcStyle fill:#593b77,stroke:#a879d7,color:#fff
    classDef botStyle fill:#1f4d3a,stroke:#42c98b,color:#fff
    classDef mcStyle fill:#444444,stroke:#aaaaaa,color:#fff

    class Top,lang,A,B topStyle
    class RPC rpcStyle
    class Bottom,node,impl botStyle
    class mc mcStyle
