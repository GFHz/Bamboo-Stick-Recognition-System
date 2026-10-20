# 竹签识别与自动计价系统

面向餐饮结算场景的全栈应用：上传竹签图片，通过 YOLO 检测数量，人工复核后生成订单，并支持门店管理与营业统计。

## 实机演示

以下为项目实际操作录屏，点击链接可查看或下载：

| 平台 | 演示视频 |
| --- | --- |
| 手机端（竖屏） | [查看手机端演示](docs/videos/mobile-demo.mp4) |
| Web 端（横屏） | [查看 Web 端演示](docs/videos/web-demo.mp4) |

视频文件保存在 `docs/videos/` 目录中。录屏展示实际项目，上述个人作品集中的手绘交互另标为流程示意。

## 功能

- JPG / PNG 图片上传、区域预处理、竹签检测和位置标注
- 识别结果人工调整，竹签与铁签计价
- 管理员与员工角色、账号认证与密码管理
- 订单查询、价格配置、员工管理、营业统计与 Excel 导出
- 图片定期清理

## 技术栈

前端：Vue 3、Vite、Element Plus、Pinia、Vue Router、ECharts、Axios。

后端：FastAPI、SQLAlchemy、Alembic、MySQL、JWT、APScheduler。

识别：Ultralytics YOLO、OpenCV、Pillow；模型路径为 `detection/best.pt`。

## 获取完整源码

完整前端、后端和 YOLO 模型已按原目录结构收录于仓库根目录的 [bamboo-vision-source.zip](bamboo-vision-source.zip)。请先下载并解压，再按下方步骤运行。

## 本地运行

建议使用 Python 3.10+、Node.js 18+，并准备 MySQL 数据库 `skewer_count`。

```powershell
cd backend
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install -r requirements.txt
Copy-Item .env.example .env
# 修改 .env 的数据库连接与 JWT_SECRET，按需配置腾讯云验证码
alembic upgrade head
uvicorn app.main:app --reload
```

另开终端：

```powershell
cd frontend
npm install
npm run dev
```

前端默认地址为 [http://localhost:5173](http://localhost:5173)，接口文档为 [http://localhost:8000/docs](http://localhost:8000/docs)。

`backend/scripts/init_db.py` 是开发重置脚本，会删除并重建数据表，且包含默认开发账号；请仅在可清空的本地测试库使用。正式环境应采用迁移、独立创建管理员并设置强密码。

## 目录

```text
backend/       API、业务服务、数据库模型与迁移
frontend/      Vue 页面与交互
detection/     检测模型权重
*.md           需求、数据库、模块与测试文档
```
