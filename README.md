# 🌤️ Weather API Service - 实时天气查询服务

基于 **Spring Boot** + **MyBatis** + **Jsoup** 构建的实时天气查询后端服务。通过爬取“中国天气网”的公开数据，提供标准化的 RESTful API 接口，并将数据持久化至 MySQL 数据库。

## ✨ 主要功能

- 🌐 **实时爬取**：通过 Jsoup 解析 HTML，实时获取指定城市的温度、天气状况、风向。
- 🗄️ **数据持久化**：使用 MyBatis + MySQL 存储天气记录，支持 `Upsert`（存在即更新，不存在即插入）。
- 📡 **RESTful API**：提供统一的 JSON 响应格式，支持跨域（CORS）请求，方便前端或移动端接入。
- ⏱️ **时间追踪**：自动记录每条天气数据的最后更新时间。

## 🛠️ 技术栈

| 技术 | 版本/说明 | 用途 |
| :--- | :--- | :--- |
| **Java** | 17 | 基础运行环境 |
| **Spring Boot** | 3.2.x (需修正) | Web 容器与 IOC 管理 |
| **MyBatis** | 4.0.1 | ORM 框架，简化数据库操作 |
| **MySQL** | 8.0+ | 关系型数据库 |
| **Jsoup** | 1.15.4 | HTML 解析与爬虫工具 |
| **Lombok** | - | 简化实体类代码 (@Data) |
| **Maven** | - | 项目构建与依赖管理 |

## 🚀 快速开始 (Quick Start)

### 1. 环境准备
- JDK 17+
- MySQL 8.0+
- Maven 3.6+

### 2. 数据库初始化
请在你的 MySQL 中执行以下建表语句：
```sql
CREATE DATABASE IF NOT EXISTS weather_db DEFAULT CHARSET utf8mb4;

USE weather_db;

CREATE TABLE IF NOT EXISTS weather_record (
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '主键ID',
    city_name VARCHAR(50) NOT NULL UNIQUE COMMENT '城市名称（唯一索引）',
    temperature VARCHAR(10) COMMENT '温度',
    weather_condition VARCHAR(50) COMMENT '天气状况',
    wind_direction VARCHAR(20) COMMENT '风向',
    humidity VARCHAR(20) COMMENT '湿度',
    update_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间'
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
