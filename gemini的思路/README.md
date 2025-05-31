
下面，我将为你规划一个从零开始开发一个可视化观星记录软件的流程，详细讲解你需要学习的东西，如何构建数据库，如何调用 API，并最终呈现一个假想的网页结构。


项目目标： 开发一个基于 Web 的观星记录应用，帮助用户分类、记录已观测的天体，并可视化观测进度。

核心需求回顾：

天体分类：每个天体可属于多个类别。

观测记录：用户可标记天体为“已观测”，记录时间、地点。

进度可视化：美观地展示各类别（含嵌套类别）的观测进度。

查询功能：按天体名称搜索；按类别搜索并查看进度及天体列表。

技术栈：Python 后端，学习基本前端技术。

开发流程规划：

这是一个典型的 Web 应用开发项目，可以分为几个主要阶段：

概念设计与需求细化 (Concept & Detail Design)

明确功能细节，绘制简单的用户流程图。

设计数据模型（数据库结构的前身），考虑如何表示天体、分类、观测记录、用户等。

规划用户界面草图 (Wireframe)，确定页面布局和交互方式。


数据采集与处理 (Data Acquisition & Processing)

确定需要哪些天体数据（名称、坐标、类型、亮度、所属目录等）。

寻找可靠的天体数据源（API 或可下载的目录文件）。

编写 Python 脚本下载、清洗和整理数据，使其符合你的数据库结构。


数据库设计与实现 (Database Design & Implementation)

根据数据模型，设计数据库表结构，定义字段、主键、外键和索引。

选择合适的数据库系统。

使用 Python ORM (Object-Relational Mapper) 或库来创建数据库和表，并将采集的数据导入。


后端开发 (Backend Development - Python)

选择 Python Web 框架 (Flask 或 Django)。

编写代码，实现用户认证（简化）、天体数据管理、观测记录管理、搜索功能、进度计算等业务逻辑。

创建 RESTful API 接口，供前端调用。


前端开发 (Frontend Development - HTML, CSS, JavaScript)

编写 HTML 结构，构建网页骨架。

编写 CSS，美化页面，实现布局和样式。

编写 JavaScript 代码，通过 API 与后端交互，动态加载数据，响应用户操作，实现进度可视化。


可视化实现 (Visualization Implementation)

选择合适的前端可视化库（如 Chart.js）。

根据后端提供的进度数据，使用 JavaScript 绘制图表（饼图、柱状图等）。


测试与部署 (Testing & Deployment)

对各功能模块进行单元测试和集成测试。

将应用部署到服务器或本地环境运行。

你需要学习的东西：

Python Web 框架：

推荐： Flask。相对于 Django 更轻量级，入门曲线平缓，适合初学者快速搭建 Web 应用，方便与基本前端技术结合。

学习内容： 如何安装和运行 Flask 应用，定义路由 (Routes)，处理 HTTP 请求 (GET, POST)，使用模板引擎 (Jinja2)，处理表单，Sessions。

数据库与 ORM：

数据库系统： SQLite 是一个非常好的起点，它是一个文件数据库，无需单独安装服务器，易于使用和学习。后期可以考虑 PostgreSQL 或 MySQL。

SQL 语言： 学习基本的 SQL 查询 (SELECT, INSERT, UPDATE, DELETE)，以及 JOIN (连接多个表查询数据)。

Python ORM： SQLAlchemy。这是一个功能强大且灵活的 ORM 库，支持多种数据库后端。它可以让你用 Python 对象的方式来操作数据库，而无需直接写 SQL。

学习内容： 数据库基本概念，SQL 基础，SQLAlchemy 的安装和使用，如何定义模型 (Models) 映射到数据库表，如何通过模型进行增删改查。

数据获取与处理：

网络请求： Python 的 requests 库。学习如何发送 GET/POST 请求，设置请求头，处理响应，特别是解析 JSON 格式的数据。

数据处理： Python 的 pandas 库（可选但推荐）。学习如何读取、处理、清洗结构化数据（如 CSV 文件）。

前端基础 (HTML, CSS, JavaScript)：

HTML5： 学习标签（语义化标签如 <header>, <nav>, <main>, <article>, <aside>, <footer>）、元素、属性、表单等。

CSS3： 学习选择器、盒模型、布局 (Flexbox, Grid)、颜色、字体、响应式设计基础。

JavaScript (ES6+)： 学习变量、数据类型、函数、控制流、DOM 操作（如何通过 JS 查找和修改 HTML 元素）、事件处理（点击、提交等）、异步编程 (Promises, async/await) 用于处理 API 请求。

与后端交互： 学习 fetch API 或 XMLHttpRequest 对象，如何在 JavaScript 中发起 HTTP 请求到你的后端 API，接收 JSON 数据并更新页面。

可视化库：

推荐： Chart.js。简单易用，文档友好，可以绘制多种常见图表（饼图、柱状图、折线图等）。

学习内容： 如何安装（通常是直接引入 CDN 或下载 JS 文件），如何在 HTML 中创建 <canvas> 元素，如何使用 JavaScript 传入数据和配置项来绘制图表。

API 概念：

理解 RESTful API 的设计原则（资源导向，使用 HTTP 方法）。

理解 JSON (JavaScript Object Notation) 数据格式，它是 Web API 中最常用的数据交换格式。

如何建立数据库：

选择 SQLite + SQLAlchemy 是一个不错的入门组合。

1. 设计数据库结构 (以 SQLite 为例)

我们定义以下几个核心表：

categories (类别表):

id (INTEGER PRIMARY KEY): 类别唯一 ID。

name (TEXT UNIQUE NOT NULL): 类别名称 (e.g., "全天88星座", "人造卫星", "恒星", "星系", "梅西耶天体", "黄道星座")。

parent_id (INTEGER): 父类别 ID，可以为 NULL（表示顶级类别）。 FOREIGN KEY 到 categories(id)。这用来实现嵌套分类。

description (TEXT): 类别描述 (可选)。

objects (天体表):

id (INTEGER PRIMARY KEY): 天体唯一 ID。

name (TEXT UNIQUE NOT NULL): 天体名称 (e.g., "北极星", "仙女座星系", "国际空间站 ISS", "M31")。

type (TEXT): 天体类型 (e.g., "Star", "Galaxy", "Satellite", "Nebula", "Planet") - 这个字段可以用来细分或作为一种特殊的分类标记。

ra (REAL): 赤经 (Right Ascension)，天球坐标。

dec (REAL): 赤纬 (Declination)，天球坐标。

magnitude (REAL): 视星等 (亮度)。

catalog_data (TEXT): 其他目录编号或数据 (JSON 格式存储，如 {"messier": "M31", "ngc": "NGC 224"}) (可选)。

description (TEXT): 天体描述 (可选)。

object_category_link (天体与类别关联表 - Many-to-Many 中间表):

object_id (INTEGER): FOREIGN KEY 到 objects(id)。

category_id (INTEGER): FOREIGN KEY 到 categories(id)。

PRIMARY KEY (object_id, category_id): 组合主键，确保同一天体在同一类别下只有一条记录。

说明： 这个表是实现“每个天体可以分到多个类中”的关键。例如，仙女座星系 (M31) 可以同时属于 "星系" 类别、"梅西耶天体" 类别，以及它所在的 "仙女座" 星座类别。

users (用户表): (简化，如果不需要多用户则跳过或简化为单用户设置)

id (INTEGER PRIMARY KEY): 用户唯一 ID。

username (TEXT UNIQUE NOT NULL).

password_hash (TEXT).

observations (观测记录表):

id (INTEGER PRIMARY KEY): 观测记录唯一 ID。

user_id (INTEGER): FOREIGN KEY 到 users(id)。(如果单用户，可以省略或固定为某个值)

object_id (INTEGER): FOREIGN KEY 到 objects(id)。

observation_time (DATETIME): 观测时间。

latitude (REAL): 观测地点纬度 (可选)。

longitude (REAL): 观测地点经度 (可选)。

notes (TEXT): 观测笔记 (可选)。

PRIMARY KEY (user_id, object_id): 考虑是否允许用户多次观测同一天体并记录多条，如果允许，则不需要 user_id 和 object_id 的组合主键，只保留 id 作为主键。如果只记录“是否已观测”，则可以在 object_user_status 表中记录 user_id, object_id, is_observed。但为了记录时间和地点，单独的 observations 表更好。

关于类别嵌套和天体分类：

你的例子 "恒星属于星系属于黄道星系" 在天文学上不准确。恒星位于星系内，但不是“属于”某个星系类别作为一种属性。黄道星系也不是一个标准的分类。

更合理的分类体系可以这样设计：

顶级类别 (Top Categories):

全天88星座 (Constellations)

梅西耶天体 (Messier Objects)

星系 (Galaxies)

星云 (Nebulae)

星团 (Star Clusters)

恒星 (Stars)

太阳系 (Solar System Objects) -> 子类别：行星、矮行星、小行星、彗星

人造天体 (Artificial Satellites)

其他...

类别嵌套 (parent_id) 示例：

id=1, name="全天88星座", parent_id=NULL

id=2, name="人造卫星", parent_id=NULL

id=3, name="深空天体", parent_id=NULL

id=4, name="星系", parent_id=3

id=5, name="星云", parent_id=3

id=6, name="梅西耶天体", parent_id=NULL

天体与类别关联 (object_category_link) 示例：

仙女座星系 (M31) 的 object_id 为 100。

类别 "星系" 的 category_id 为 4。

类别 "梅西耶天体" 的 category_id 为 6。

类别 "仙女座" (假设其 category_id 为 70，parent_id 为 1)

object_category_link 表中会有：

(object_id=100, category_id=4)

(object_id=100, category_id=6)

(object_id=100, category_id=70)

这样就实现了 M31 同时属于多个类别。

2. 使用 SQLAlchemy 创建数据库和表

安装 SQLAlchemy：pip install sqlalchemy

简单的代码示例 (models.py):

from sqlalchemy import create_engine, Column, Integer, String, Float, DateTime, ForeignKey, Table
from sqlalchemy.orm import declarative_base, relationship, sessionmaker
from sqlalchemy.sql import func # 用于获取当前时间等

# 定义数据库连接 URL
DATABASE_URL = "sqlite:///stellar_trail.db" # 使用 SQLite 数据库文件

# 创建数据库引擎
engine = create_engine(DATABASE_URL)

# 创建一个基类，其他模型类将继承它
Base = declarative_base()

# 定义 Many-to-Many 关联表
object_category_link = Table(
    'object_category_link', Base.metadata,
    Column('object_id', Integer, ForeignKey('objects.id'), primary_key=True),
    Column('category_id', Integer, ForeignKey('categories.id'), primary_key=True)
)

# 定义模型类 (对应数据库表)
class Category(Base):
    __tablename__ = 'categories'

    id = Column(Integer, primary_key=True)
    name = Column(String, unique=True, nullable=False)
    parent_id = Column(Integer, ForeignKey('categories.id'))
    description = Column(String)

    # 建立父子关系，可以方便地查询子类别或父类别
    parent = relationship("Category", remote_side=[id])
    children = relationship("Category", backref="parent") # 方便通过 parent.children 获取子类

    # 通过 Many-to-Many 关联获取该类别下的所有天体
    objects = relationship("Object", secondary=object_category_link, back_populates="categories")

    def __repr__(self):
        return f"<Category(name='{self.name}')>"

class Object(Base):
    __tablename__ = 'objects'

    id = Column(Integer, primary_key=True)
    name = Column(String, unique=True, nullable=False)
    type = Column(String) # e.g., 'Star', 'Galaxy'
    ra = Column(Float)
    dec = Column(Float)
    magnitude = Column(Float)
    catalog_data = Column(String) # Consider using JSONB type in PostgreSQL if needed
    description = Column(String)

    # 通过 Many-to-Many 关联获取该天体所属的所有类别
    categories = relationship("Category", secondary=object_category_link, back_populates="objects")

    # 获取该天体的所有观测记录
    observations = relationship("Observation", back_populates="object")

    def __repr__(self):
        return f"<Object(name='{self.name}', type='{self.type}')>"

# class User(Base): # 如果需要多用户，可以定义用户表
#     __tablename__ = 'users'
#     id = Column(Integer, primary_key=True)
#     username = Column(String, unique=True, nullable=False)
#     password_hash = Column(String)
#     observations = relationship("Observation", back_populates="user")


class Observation(Base):
    __tablename__ = 'observations'

    id = Column(Integer, primary_key=True)
    # user_id = Column(Integer, ForeignKey('users.id')) # 如果单用户，可以省略或注释掉
    object_id = Column(Integer, ForeignKey('objects.id'), nullable=False)
    observation_time = Column(DateTime, default=func.now()) # 默认当前时间
    latitude = Column(Float)
    longitude = Column(Float)
    notes = Column(String)

    # user = relationship("User", back_populates="observations") # 如果单用户，可以省略或注释掉
    object = relationship("Object", back_populates="observations")

    def __repr__(self):
        return f"<Observation(object='{self.object.name if self.object else 'N/A'}', time='{self.observation_time}')>"

# 创建所有表
# 在 Python 脚本中运行一次即可创建数据库文件和表
if __name__ == "__main__":
    Base.metadata.create_all(engine)
    print("数据库表已创建!")

    # 示例：添加一些类别和天体
    Session = sessionmaker(bind=engine)
    session = Session()

    # 添加顶级类别
    cat_constellations = Category(name="全天88星座")
    cat_deepsky = Category(name="深空天体")
    cat_artificial = Category(name="人造天体")
    cat_messier = Category(name="梅西耶天体") # M天体也是深空天体

    session.add_all([cat_constellations, cat_deepsky, cat_artificial, cat_messier])
    session.commit()

    # 添加子类别 (星系，父类别是深空天体)
    cat_galaxies = Category(name="星系", parent=cat_deepsky)
    session.add(cat_galaxies)
    session.commit() # 提交以便获取新创建类别的ID

    # 刷新以确保获取到最新的类别对象和ID
    session.refresh(cat_constellations)
    session.refresh(cat_deepsky)
    session.refresh(cat_artificial)
    session.refresh(cat_messier)
    session.refresh(cat_galaxies)


    # 添加天体 (例如：仙女座星系 M31)
    obj_m31 = Object(name="仙女座星系", type="Galaxy", ra=10.6847, dec=41.2690, magnitude=3.4)
    session.add(obj_m31)
    session.commit()
    session.refresh(obj_m31)

    # 将 M31 与多个类别关联
    m31_link_galaxy = object_category_link.insert().values(object_id=obj_m31.id, category_id=cat_galaxies.id)
    m31_link_messier = object_category_link.insert().values(object_id=obj_m31.id, category_id=cat_messier.id)
    # 假设已经创建了“仙女座”这个星座类别 (其 parent_id 是 cat_constellations.id)
    # 需要查找或创建“仙女座”类别
    cat_andromeda = session.query(Category).filter_by(name="仙女座").first()
    if not cat_andromeda:
         cat_andromeda = Category(name="仙女座", parent=cat_constellations)
         session.add(cat_andromeda)
         session.commit()
         session.refresh(cat_andromeda)
    m31_link_andromeda = object_category_link.insert().values(object_id=obj_m31.id, category_id=cat_andromeda.id)

    # 执行插入关联数据的操作
    session.execute(m31_link_galaxy)
    session.execute(m31_link_messier)
    session.execute(m31_link_andromeda)
    session.commit()


    # 添加一个人造卫星 (例如：国际空间站 ISS)
    obj_iss = Object(name="国际空间站 ISS", type="Satellite") # RA/Dec/Magnitude 对卫星不固定
    session.add(obj_iss)
    session.commit()
    session.refresh(obj_iss)

    # 将 ISS 与人造天体类别关联
    iss_link_artificial = object_category_link.insert().values(object_id=obj_iss.id, category_id=cat_artificial.id)
    session.execute(iss_link_artificial)
    session.commit()

    # 示例：记录观测 M31
    # 假设单用户，user_id=1 (如果有多用户，需要先创建用户)
    # obs_m31 = Observation(user_id=1, object=obj_m31, latitude=34.0522, longitude=-118.2437, notes="Great view tonight!") # 多用户版本
    obs_m31 = Observation(object=obj_m31, latitude=34.0522, longitude=-118.2437, notes="Great view tonight!") # 单用户版本
    session.add(obs_m31)
    session.commit()

    session.close()
    print("示例数据已添加!")


这个脚本可以作为你的 models.py 文件。运行一次 python models.py 就会创建一个 stellar_trail.db 文件和相应的表。

3. 数据导入

你需要找到可靠的天体数据源。一些思路：

对于标准星表/天体列表 (Messier, NGC, Constellations)： 查找公开的 CSV 或 JSON 文件。例如，维基百科常有这类列表，可能需要手动整理或编写爬虫（注意遵守网站规则）。有很多天文学网站也提供数据下载。

对于恒星： 像 Hipparcos, Gaia 这样的星表非常庞大，你可能需要一个子集或者通过 API 查询。

对于人造卫星： Space-Track.org 提供 TLE (Two-Line Elements) 数据，但这通常用于计算当前位置，而不是提供一个静态列表。你可以找到一些流行的卫星列表。

找到数据后，编写 Python 脚本，使用 pandas 或纯 Python 代码读取数据文件，然后使用 SQLAlchemy 将数据批量插入到 objects 和 object_category_link 表中。

如何调用各种 API：

你主要需要调用 API 来获取天体数据。上面提到的 SIMBAD、JPL Horizons 等都有 API 接口，但它们的复杂度和数据类型不同。

示例：使用 requests 调用一个假想的天体 API

假设有一个简单的 API https://api.astrostuff.com/object?name=M31 返回 M31 的 JSON 数据：

{
  "name": "仙女座星系",
  "id": "M31",
  "type": "Galaxy",
  "ra": 10.6847,
  "dec": 41.2690,
  "magnitude": 3.4,
  "constellation": "Andromeda",
  "catalogs": ["Messier", "NGC"]
}
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Json
IGNORE_WHEN_COPYING_END

使用 Python requests 调用：

import requests

def get_object_data_from_api(object_name):
    base_url = "https://api.astrostuff.com/object" # 假想的API地址
    params = {'name': object_name}
    try:
        response = requests.get(base_url, params=params)
        response.raise_for_status() # 如果请求失败（非200状态码），抛出异常
        data = response.json() # 解析JSON响应体
        return data
    except requests.exceptions.RequestException as e:
        print(f"API 请求失败: {e}")
        return None

# 示例调用
object_info = get_object_data_from_api("M31")
if object_info:
    print(f"获取到天体数据: {object_info['name']}, RA: {object_info['ra']}, Dec: {object_info['dec']}")
    # 可以将这些数据存入数据库
    # ... (使用SQLAlchemy session 添加到数据库)
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Python
IGNORE_WHEN_COPYING_END

注意： 实际的天文数据库 API 可能更复杂，需要注册、API Key，或者使用特定的查询语言（如 SIMBAD 的 CDS Service）。对于初学者，直接下载并导入一个整理好的静态星表（如 Messier Catalog 的 CSV 文件）可能是更简单的起点，API 可以留到后期用于获取实时数据（如卫星位置）或补充数据。

实现进度可视化：

进度可视化需要在后端计算数据，在前端使用 JavaScript 库绘制。

后端计算进度 (Flask + SQLAlchemy):
在 Flask 后端，你需要一个 API 接口来计算某个类别的观测进度。

编写一个函数，接受 category_id 作为参数。

通过 SQLAlchemy 查询，找到属于该类别的所有天体的 ID 列表 (object_category_link 表)。

通过 SQLAlchemy 查询，计算当前用户（如果有多用户）已观测的、且属于该类别的天体数量 (observations 表与天体 ID 列表关联)。

计算总天体数量 (上一步的天体 ID 列表长度)。

进度 = (已观测数量 / 总数量) * 100%。

将总数量、已观测数量、进度百分比等数据打包成 JSON 格式返回。

关于嵌套类别的进度计算： 如果一个类别包含子类别，计算该类别下的总天体数量，可以选择两种方式：

仅计算直接属于该类别的天体： 只统计 object_category_link 中 category_id 直接等于目标类别的天体。

计算包含所有子类别的天体： 递归地查找该类别下的所有子类别，然后统计直接或间接属于这些所有类别中的任一个的天体。这需要更复杂的 SQL 查询（例如使用 Common Table Expressions - CTE）或在 Python 中递归处理。对于初学者，可以先从计算直接属于某类别的天体开始。计算总天体数量和已观测数量的逻辑类似。

示例 Flask API 伪代码:

# app.py (Flask 应用文件)
from flask import Flask, jsonify, request
from models import Session, Category, Object, Observation, object_category_link, engine
from sqlalchemy import func, distinct # 引入 func 和 distinct

app = Flask(__name__)
SessionLocal = sessionmaker(bind=engine)

def get_category_progress(category_id):
    session = SessionLocal()
    try:
        # Option 1: Calculate progress ONLY for objects directly linked to this category
        total_objects_in_category = session.query(func.count(object_category_link.c.object_id)).filter(
            object_category_link.c.category_id == category_id
        ).scalar()

        if total_objects_in_category is None or total_objects_in_category == 0:
            return {"total": 0, "observed": 0, "progress": 0.0}

        # Find IDs of objects directly in this category
        object_ids_in_category = session.query(object_category_link.c.object_id).filter(
            object_category_link.c.category_id == category_id
        ).subquery()

        # Count observed objects within these IDs (assuming single user for simplicity)
        observed_objects_count = session.query(func.count(distinct(Observation.object_id))).filter(
             # Observation.user_id == current_user_id, # 如果有多用户
             Observation.object_id.in_(object_ids_in_category)
        ).scalar()

        progress_percentage = (observed_objects_count / total_objects_in_category) * 100 if total_objects_in_category > 0 else 0

        return {
            "category_id": category_id,
            "total": total_objects_in_category,
            "observed": observed_objects_count,
            "progress": round(progress_percentage, 2) # 保留两位小数
        }
    finally:
        session.close()

@app.route('/api/categories/<int:category_id>/progress', methods=['GET'])
def get_category_progress_api(category_id):
    progress_data = get_category_progress(category_id)
    return jsonify(progress_data)

# --- 其他API路由 (搜索, 天体列表, 记录观测等) ---
@app.route('/api/objects/search', methods=['GET'])
def search_objects():
    query = request.args.get('q', '') # 获取查询参数 q
    if not query:
        return jsonify([]) # 查询为空返回空列表

    session = SessionLocal()
    try:
        # 使用 LIKE 进行模糊搜索名称
        results = session.query(Object).filter(Object.name.like(f"%{query}%")).limit(20).all() # 限制结果数量
        # 将查询结果转换为字典列表返回
        objects_list = [{"id": obj.id, "name": obj.name, "type": obj.type, "ra": obj.ra, "dec": obj.dec} for obj in results]
        return jsonify(objects_list)
    finally:
        session.close()

@app.route('/api/observations', methods=['POST'])
def log_observation():
    data = request.get_json() # 获取前端发送的JSON数据
    object_id = data.get('object_id')
    # user_id = current_user_id # 如果有多用户
    latitude = data.get('latitude')
    longitude = data.get('longitude')
    notes = data.get('notes')

    if not object_id:
        return jsonify({"error": "Missing object_id"}), 400

    session = SessionLocal()
    try:
        # 检查天体是否存在
        obj = session.query(Object).get(object_id)
        if not obj:
             return jsonify({"error": "Object not found"}), 404

        # 创建新的观测记录
        # new_observation = Observation(user_id=user_id, object_id=object_id, latitude=latitude, longitude=longitude, notes=notes) # 多用户
        new_observation = Observation(object_id=object_id, latitude=latitude, longitude=longitude, notes=notes) # 单用户
        session.add(new_observation)
        session.commit()
        return jsonify({"message": "Observation logged successfully", "observation_id": new_observation.id}), 201
    except Exception as e:
        session.rollback()
        return jsonify({"error": str(e)}), 500
    finally:
        session.close()


if __name__ == '__main__':
    # 确保数据库和表已创建 (可以在应用启动时检查或单独运行models.py)
    # Base.metadata.create_all(engine)
    app.run(debug=True) # 启动开发服务器
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Python
IGNORE_WHEN_COPYING_END

前端调用 API 并绘制图表 (JavaScript + Chart.js):

安装 Chart.js (通过 CDN 或下载)：
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>

在 HTML 中创建一个 <canvas> 元素作为图表容器：
<canvas id="progressChart" width="400" height="200"></canvas>

使用 JavaScript 调用后端 API，获取数据，并绘制图表：

// script.js

// 假设你有一个函数可以获取当前选中的类别ID
function getSelectedCategoryId() {
    // 从页面元素 (如下拉框或点击的类别链接) 获取类别ID
    return 1; // 示例: 获取类别ID为1的数据 (例如，“全天88星座”)
}

async function loadProgressChart(categoryId) {
    const canvas = document.getElementById('progressChart');
    if (!canvas) return;

    const url = `/api/categories/${categoryId}/progress`; // 调用后端API

    try {
        const response = await fetch(url); // 发起GET请求
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json(); // 解析JSON响应

        const total = data.total;
        const observed = data.observed;
        const unobserved = total - observed;

        // 绘制饼图
        new Chart(canvas, {
            type: 'pie', // 图表类型: 饼图
            data: {
                labels: ['已观测', '未观测'], // 数据标签
                datasets: [{
                    label: '观测进度',
                    data: [observed, unobserved], // 数据值
                    backgroundColor: [
                        'rgba(75, 192, 192, 0.6)', // 已观测颜色 (例如青色)
                        'rgba(255, 99, 132, 0.6)' // 未观测颜色 (例如红色)
                    ],
                    borderColor: [
                        'rgba(75, 192, 192, 1)',
                        'rgba(255, 99, 132, 1)'
                    ],
                    borderWidth: 1
                }]
            },
            options: {
                responsive: true, // 图表尺寸自适应容器
                plugins: {
                    title: {
                        display: true,
                        text: `类别观测进度 (总数: ${total}, 已观测: ${observed})` // 图表标题
                    },
                    tooltip: { // 鼠标悬停提示
                        callbacks: {
                            label: function(context) {
                                const label = context.label || '';
                                if (label) {
                                    const value = context.raw;
                                    const percentage = ((value / total) * 100).toFixed(2) + '%';
                                    return `${label}: ${value} (${percentage})`;
                                }
                                return '';
                            }
                        }
                    }
                }
            }
        });

    } catch (error) {
        console.error("加载图表数据失败:", error);
        // 可以在页面上显示错误信息
    }
}

// 在页面加载完成后调用函数加载图表 (示例: 加载类别ID为1的进度)
document.addEventListener('DOMContentLoaded', () => {
    const initialCategoryId = getSelectedCategoryId();
    if (initialCategoryId) {
        loadProgressChart(initialCategoryId);
    }
     // --- 其他前端逻辑，如加载类别列表，设置点击事件等 ---
});

// --- 实现搜索功能的示例 ---
async function performSearch() {
    const searchInput = document.getElementById('searchInput');
    const resultsDiv = document.getElementById('searchResults');
    const query = searchInput.value;

    if (!query) {
        resultsDiv.innerHTML = ''; // 清空结果
        return;
    }

    const url = `/api/objects/search?q=${encodeURIComponent(query)}`; // 调用搜索API

    try {
        const response = await fetch(url);
        if (!response.ok) {
             throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json(); // 解析结果列表

        // 显示搜索结果
        resultsDiv.innerHTML = ''; // 清空旧结果
        if (data.length === 0) {
            resultsDiv.innerHTML = '<p>未找到相关天体。</p>';
        } else {
            const ul = document.createElement('ul');
            data.forEach(obj => {
                const li = document.createElement('li');
                li.textContent = `${obj.name} (${obj.type})`;
                // 可以添加链接到天体详情页或一个“记录观测”按钮
                ul.appendChild(li);
            });
            resultsDiv.appendChild(ul);
        }

    } catch(error) {
         console.error("搜索失败:", error);
         resultsDiv.innerHTML = '<p>搜索时发生错误。</p>';
    }
}

// 将搜索功能绑定到输入框变化或按钮点击事件 (例如，给搜索框添加一个 input 事件监听器)
// const searchInput = document.getElementById('searchInput');
// searchInput.addEventListener('input', performSearch); // 输入时即时搜索
// 或者绑定到一个搜索按钮的点击事件
// const searchButton = document.getElementById('searchButton');
// searchButton.addEventListener('click', performSearch);


// --- 实现记录观测的示例 ---
async function logObservation(objectId) {
     const url = '/api/observations'; // 调用记录观测API
     const data = {
         object_id: objectId,
         // latitude: ..., // 可以从浏览器获取位置信息或让用户输入
         // longitude: ...,
         // notes: "用户输入的笔记"
     };

     try {
         const response = await fetch(url, {
             method: 'POST', // 使用POST方法
             headers: {
                 'Content-Type': 'application/json' // 告诉后端发送的是JSON数据
             },
             body: JSON.stringify(data) // 将JS对象转换为JSON字符串
         });

         const result = await response.json();

         if (response.ok) {
             alert(result.message); // 记录成功提示
             // 记录成功后，可能需要刷新页面上的状态或进度条
         } else {
             alert("记录观测失败: " + result.error); // 记录失败提示
         }

     } catch (error) {
         console.error("记录观测时发生错误:", error);
         alert("记录观测时发生网络错误。");
     }
}
// 在页面中给每个天体添加一个“记录观测”按钮，点击时调用这个函数
// 例如 <button onclick="logObservation(100)">记录观测</button>
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
JavaScript
IGNORE_WHEN_COPYING_END

假网页结构 (HTML 伪代码):

创建一个 index.html 文件：

<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>星辰足迹 - 观星记录</title>
    <!-- 引入 CSS 文件 -->
    <link rel="stylesheet" href="style.css">
    <!-- 引入 Chart.js 库 -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
</head>
<body>

    <header>
        <h1>星辰足迹</h1>
        <nav>
            <!-- 导航链接 -->
            <a href="#">首页</a>
            <a href="#">我的记录</a>
            <a href="#">天体目录</a>
            <!-- 可以有用户登录/注册链接 -->
        </nav>
    </header>

    <main>
        <aside class="sidebar">
            <!-- 类别导航区域 -->
            <h2>天体类别</h2>
            <ul id="categoryList">
                <!-- 这里会通过JS从后端加载类别列表 -->
                <li><a href="#" data-category-id="1">全天88星座</a></li>
                <li><a href="#" data-category-id="3">深空天体</a>
                    <ul>
                        <li><a href="#" data-category-id="4">星系</a></li>
                        <li><a href="#" data-category-id="5">星云</a></li>
                    </ul>
                </li>
                 <li><a href="#" data-category-id="6">梅西耶天体</a></li>
                <!-- ... 更多类别 -->
            </ul>
        </aside>

        <section class="content">
            <!-- 主要内容区域 -->

            <div class="search-section">
                <h2>搜索天体</h2>
                <input type="text" id="searchInput" placeholder="输入天体名称...">
                <button id="searchButton">搜索</button>
                <div id="searchResults">
                    <!-- 搜索结果会显示在这里 -->
                </div>
            </div>

            <div class="category-view" id="categoryView">
                <!-- 当前选中类别的视图 -->
                <h2 id="categoryName">请选择一个类别</h2>

                <div class="progress-chart">
                    <h3>观测进度</h3>
                    <!-- 进度图表会绘制在这里 -->
                    <canvas id="progressChart" width="400" height="200"></canvas>
                </div>

                <div class="object-list">
                    <h3>类别天体列表</h3>
                    <ul id="objectList">
                        <!-- 该类别下的天体列表会显示在这里 -->
                        <!-- 示例列表项 -->
                        <li>仙女座星系 (Galaxy) - <button onclick="logObservation(100)">记录观测</button></li>
                        <li>M32 (Galaxy) - <button onclick="logObservation(101)">记录观测</button></li>
                        <!-- ... -->
                    </ul>
                </div>

            </div>

            <!-- 可以有其他视图区域，如“我的观测记录”页面 -->

        </section>
    </main>

    <footer>
        <p>© 2023 星辰足迹</p>
    </footer>

    <!-- 引入 JavaScript 文件 -->
    <script src="script.js"></script>
    <script>
        // 在 script.js 中实现加载类别列表和处理点击事件的代码
        // 例如：
        // document.querySelectorAll('#categoryList a').forEach(link => {
        //     link.addEventListener('click', (e) => {
        //         e.preventDefault();
        //         const categoryId = e.target.dataset.categoryId;
        //         const categoryName = e.target.textContent;
        //         document.getElementById('categoryName').textContent = categoryName;
        //         loadProgressChart(categoryId); // 加载进度图
        //         loadObjectsInCategory(categoryId); // 加载天体列表 (需要另外实现一个API和前端函数)
        //     });
        // });

        // 示例：初次加载时显示某个类别的视图
        // document.addEventListener('DOMContentLoaded', () => {
        //     const defaultCategoryId = 1; // 假设默认显示类别ID为1
        //     const defaultCategoryName = "全天88星座"; // 需要从后端获取类别名称或者写死
        //     document.getElementById('categoryName').textContent = defaultCategoryName;
        //     loadProgressChart(defaultCategoryId);
        //     loadObjectsInCategory(defaultCategoryId); // 需要实现
        // });

        // 需要实现 loadObjectsInCategory(categoryId) 函数来获取并显示类别的天体列表
        // 这个函数会调用一个新的后端API，如 /api/categories/<id>/objects
    </script>
</body>
</html>
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Html
IGNORE_WHEN_COPYING_END

创建一个 style.css 文件来美化页面 (示例 CSS 伪代码):

/* style.css */
body {
    font-family: sans-serif;
    margin: 0;
    background-color: #f4f4f4; /* 淡灰色背景 */
    color: #333;
}

header {
    background-color: #2c3e50; /* 深蓝色 */
    color: white;
    padding: 1rem;
    text-align: center;
}

nav a {
    color: white;
    margin: 0 1rem;
    text-decoration: none;
}

main {
    display: flex; /* 使用 Flexbox 布局 */
    max-width: 1200px; /* 限制主体内容宽度 */
    margin: 1rem auto; /* 居中并添加外边距 */
    background-color: #fff; /* 白色背景 */
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1); /* 添加阴影 */
}

.sidebar {
    width: 250px; /* 侧边栏宽度 */
    padding: 1rem;
    border-right: 1px solid #ddd; /* 右边框 */
}

.sidebar ul {
    list-style: none; /* 移除列表默认样式 */
    padding: 0;
}

.sidebar li {
    margin-bottom: 0.5rem;
}

.sidebar a {
    text-decoration: none;
    color: #333;
    display: block; /* 让链接填充整个列表项宽度 */
    padding: 0.3rem 0;
}

.sidebar a:hover {
    color: #3498db; /* 鼠标悬停变色 */
}

.sidebar ul ul { /* 子类别列表缩进 */
    padding-left: 1rem;
    margin-top: 0.3rem;
}


.content {
    flex-grow: 1; /* 主要内容区域填充剩余空间 */
    padding: 1rem;
}

.search-section, .category-view {
    margin-bottom: 2rem; /* 部分之间添加间距 */
    padding: 1rem;
    border: 1px solid #eee;
    border-radius: 8px;
}

.progress-chart {
    margin-top: 1rem;
    text-align: center; /* 图表居中 */
}

.object-list ul {
    list-style: disc; /* 圆点列表 */
    padding-left: 20px;
}

footer {
    text-align: center;
    padding: 1rem;
    margin-top: 2rem;
    background-color: #2c3e50;
    color: white;
}

/* 可以添加更多样式，例如按钮样式，输入框样式等 */
IGNORE_WHEN_COPYING_START
content_copy
download
Use code with caution.
Css
IGNORE_WHEN_COPYING_END


天体坐标 (RA/Dec)： 这些是球坐标系中的角度。如果你想实现更高级的功能，比如计算两个天体之间的角距离，或者根据用户的经纬度和时间计算某个天体的地平坐标（方位角和高度角，用于判断是否可见），你需要应用球面三角学和天文坐标系转换的知识。Python 的 astropy 库提供了强大的天文学计算功能，包括坐标转换。

卫星轨迹： 如果你想记录人造卫星，获取 TLE 数据后，计算其随时间的精确位置需要复杂的轨道力学计算。这可能超出了入门范围，但了解其原理会很有趣。

可视化数据： 除了进度饼图，你还可以用其他方式可视化数据，比如用散点图展示一个类别中天体的亮度和类型分布，或者在地图上标记观测地点。这些都涉及到数据可视化和统计图表的数学原理。

数据库查询优化： 随着天体数据量增大，如何编写高效的 SQL 查询（特别是涉及 JOIN 和子查询时）会成为关键。理解查询执行计划和索引的原理，你的逻辑思维能力会很有帮助。

总结：

整个项目从概念到实现，是一个将你的数理知识与编程技能相结合的绝佳机会。

从数据库设计开始： 这是基础，想清楚天体、分类、观测记录等实体之间的关系，特别是多对多关系和类别嵌套。SQLAlchemy 会帮你用 Python 优雅地操作数据库。

数据是核心： 花时间寻找、整理和导入天体数据。

后端构建 API： 使用 Flask 搭建后端，实现数据查询、搜索和观测记录功能。

前端呈现与交互： 学习 HTML, CSS, JavaScript，构建用户界面，通过 fetch 调用后端 API，使用 Chart.js 等库进行可视化。

不要一开始就追求完美和所有功能。建议先实现核心的“天体列表 -> 查看天体详情 -> 记录观测 -> 查看单个类别进度”流程。逐步完善功能，增加更多数据和更复杂的分类/可视化。

祝你开发顺利，享受这个结合兴趣与专业知识的项目！