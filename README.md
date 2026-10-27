# 简历系统

> 🎓 **计算机毕业设计 · 简历系统**
>
> 本仓库只放**项目介绍 + 运行截图**（截图是站点带水印的原图，存在仓库 `images/` 里）。
>
> 👉 **完整可运行源码 / 数据库脚本 / 部署文档：[点我获取](https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github)**
>
> 💬 咨询微信：**ir9372**　|　🌐 更多项目：[极客代码 geekcode.top](https://geekcode.top/?utm_source=github)
>
> 📌 项目详情页：<https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github>


<table><td width="230" align="center"><a href="https://geekcode.top/?utm_source=github"><img src="images/34.jpg" alt="微信名片" width="220"></a><br><b>扫码加微信 ir9372</b></td><td valign="middle">📦 源码 = 项目介绍 + 全部运行截图 + 数据库 + 部署文档<br>👉 点上方任意截图，直接跳到 <b>极客代码 geekcode.top</b> 详情页</td></table>

---

<h1>简历系统</h1>
<h2>项目概述</h2>
<p>本项目为“简历系统”，旨在构建一个集简历管理、招聘对接与求职交流于一体的综合性服务平台。系统核心功能涵盖简历模板展示、在线简历上传、招聘会报名、求职论坛互动及系统公告发布等模块，适用于求职者完善个人职业档案、浏览招聘信息并参与社区讨论的场景。技术架构采用前后端分离模式，后端基于 Spring Boot 框架结合 MyBatis-Plus 实现高效数据持久化，使用 Shiro 进行安全权限控制；前端界面通过 Vue 集成方案呈现，提供流畅的用户交互体验。该系统有效解决了传统求职过程中信息分散、简历格式不规范及沟通渠道单一的问题，提升了人岗匹配效率。</p>
<h2>技术架构</h2>
<h3>1. 总体架构设计</h3>
<p>系统采用经典的分层架构设计，逻辑上分为表现层、业务逻辑层和数据访问层。整体遵循 RESTful API 设计规范，确保前后端通信的标准化与解耦。</p>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/01.jpg" alt="架构图"></a></p>
<h3>2. 核心技术选型理由</h3>
<ul>
<li><strong>后端框架 (Spring Boot)</strong>：利用其自动配置特性快速搭建微服务基础，简化了 XML 配置流程，提高了开发效率与维护性。<code>spring-boot-starter-web</code> 提供了内嵌 Tomcat 服务器，支持独立部署。</li>
<li><strong>ORM 框架 (MyBatis-Plus)</strong>：在 MyBatis 基础上增强了 CRUD 操作能力，通过 <code>mybatis-plus</code> 和 <code>mybatisplus-spring-boot-starter</code> 依赖，实现了单表操作的零 SQL 编写，同时保留了复杂查询的灵活性，适配本系统中简历、论坛等多实体关联场景。</li>
<li><strong>安全框架 (Apache Shiro)</strong>：选用 <code>shiro-spring</code> 进行身份认证与授权管理。相较于其他安全框架，Shiro 轻量且易于理解，能够精准控制前台用户与后台管理员的访问权限，保障系统数据安全。</li>
<li><strong>数据库连接</strong>：使用 <code>mysql-connector-java</code> 作为 JDBC 驱动，配合 <code>spring-boot-starter-jdbc</code> 实现稳定的数据源管理与事务控制。</li>
<li><strong>辅助组件</strong>：引入 <code>commons-lang3</code> 处理通用工具类需求，<code>validation-api</code> 用于后端参数校验，确保输入数据的合法性；<code>protobuf-java</code> 可能用于特定高性能数据传输或序列化场景（具体视内部模块而定）。</li>
</ul>
<h3>3. 数据库设计要点</h3>
<p>数据库主要围绕用户行为与内容管理进行建模。核心实体包括用户 (<code>yonghu</code>)、简历模板 (<code>jianlimoban</code>)、简历上传记录 (<code>jianlishangchuan</code>)、招聘会 (<code>zhaopinhui</code>)、报名记录 (<code>baomingzhaopin</code>)、论坛帖子 (<code>forum</code>)、公告 (<code>news</code>) 以及收藏记录 (<code>storeup</code>)。各表之间通过外键或业务 ID 建立关联，例如“简历上传”关联“用户”与“模板类型”，“报名招聘”关联“用户”与“招聘会”。</p>
<h2>功能模块</h2>
<h3>1. 前台用户端功能</h3>
<p>前台面向普通求职者，提供以下核心服务：</p>
<ul>
<li><strong>用户认证模块</strong>：包含注册与登录功能，支持新账号创建及已有账号的身份验证。</li>
<li><strong>简历资源中心</strong>：</li>
<li><strong>简历模板</strong>：展示各类标准简历模板供用户预览下载，支持按模板类型筛选。</li>
<li><strong>简历上传</strong>：允许用户上传个人制作的简历文件，并进行列表化管理与详情查看。</li>
<li><strong>招聘互动模块</strong>：</li>
<li><strong>招聘会</strong>：展示近期举办的招聘会信息，支持查看详情。</li>
<li><strong>报名招聘</strong>：用户可对感兴趣的招聘会发起报名申请，并查看自己的报名状态与详情。</li>
<li><strong>社区与信息模块</strong>：</li>
<li><strong>求职论坛</strong>：提供发帖、浏览帖子列表及查看帖子详情的功能，促进求职者间经验交流。</li>
<li><strong>系统公告</strong>：展示平台发布的最新通知与政策调整信息。</li>
<li><strong>在线客服</strong>：提供即时通讯入口，方便用户咨询问题。</li>
<li><strong>个人中心</strong>：</li>
<li><strong>我的发布</strong>：查看用户在论坛或其他板块发布的内容。</li>
<li><strong>我的收藏</strong>：管理用户收藏的简历模板、帖子等资源。</li>
</ul>
<h3>2. 后台管理端功能</h3>
<p>后台面向系统管理员，负责全局数据维护与业务监管：</p>
<ul>
<li><strong>用户管理</strong>：对注册用户信息进行增删改查及状态管理。</li>
<li><strong>内容管理</strong>：</li>
<li><strong>简历模板管理</strong>：维护模板库，包括新增、编辑、删除模板信息及分类。</li>
<li><strong>模板类型管理</strong>：定义和管理简历模板的分类标签。</li>
<li><strong>系统公告管理</strong>：发布、修改或删除前台展示的公告内容。</li>
<li><strong>轮播图管理</strong>：配置首页展示的动态图片资源。</li>
<li><strong>业务数据管理</strong>：</li>
<li><strong>招聘会管理</strong>：录入和维护招聘会的基本信息与日程安排。</li>
<li><strong>报名招聘管理</strong>：审核与统计用户的招聘会报名记录。</li>
<li><strong>简历上传管理</strong>：监控用户上传的简历文件，确保合规性。</li>
<li><strong>求职论坛管理</strong>：审核论坛帖子，处理违规内容，维护社区秩序。</li>
<li><strong>我的收藏管理</strong>：查看和分析用户的收藏行为数据。</li>
<li><strong>系统配置</strong>：通过 <code>/config</code> 路由对应的功能模块，对系统基础参数进行设置。</li>
<li><strong>客服管理</strong>：通过 <code>/chat</code> 路由对应模块，管理员可接入在线客服会话，回复用户咨询。</li>
</ul>
<h2>用户角色与权限</h2>
<p>根据源码中的 Controller 分布及 Shiro 安全机制，系统主要划分为两类角色：</p>
<h3>1. 普通用户 (前台)</h3>
<ul>
<li><strong>访问范围</strong>：仅限前台路由及相关公开接口。</li>
<li><strong>具体权限</strong>：</li>
<li><strong>基础操作</strong>：注册、登录、退出。</li>
<li><strong>浏览与搜索</strong>：查看简历模板、招聘会、系统公告、论坛帖子、模板类型列表。</li>
<li><strong>交互操作</strong>：上传简历、报名招聘会、在论坛发帖/评论、收藏资源、使用在线客服。</li>
<li><strong>个人数据管理</strong>：查看个人中心信息、管理“我的发布”内容、管理“我的收藏”列表、查看自己的“报名招聘”详情。</li>
</ul>
<h3>2. 管理员 (后台)</h3>
<ul>
<li><strong>访问范围</strong>：拥有后台所有路由 (<code>/admin/*</code>) 及相应 API 接口的完全控制权。</li>
<li><strong>具体权限</strong>：</li>
<li><strong>用户管理</strong>：对用户 (<code>/yonghu</code>) 数据进行全量 CRUD 操作。</li>
<li><strong>内容运营</strong>：对简历模板 (<code>/jianlimoban</code>)、模板类型 (<code>/mobanleixing</code>)、系统公告 (<code>/news</code>)、轮播图进行增删改查。</li>
<li><strong>业务监管</strong>：管理招聘会 (<code>/zhaopinhui</code>)、审核报名记录 (<code>/baomingzhaopin</code>)、监控简历上传 (<code>/jianlishangchuan</code>)、管理论坛内容 (<code>/forum</code>) 及收藏数据 (<code>/storeup</code>)。</li>
<li><strong>系统维护</strong>：修改系统配置 (<code>/config</code>)，参与在线客服对话 (<code>/chat</code>)。</li>
</ul>
<h2>项目特色与创新点</h2>
<ol>
<li><strong>全流程闭环服务</strong>：系统不仅仅提供静态的简历模板下载，还打通了“模板选择 -&gt; 简历制作/上传 -&gt; 招聘会浏览 -&gt; 在线报名 -&gt; 论坛交流”的完整求职链路，实现了从准备到行动的一站式支持。</li>
<li><strong>灵活的模板管理体系</strong>：引入了“模板类型” (<code>Mobanleixing</code>) 作为独立实体进行管理，使得简历模板的分类更加动态和可扩展，便于后续增加新的行业或风格模板类别。</li>
<li><strong>双向互动机制</strong>：除了传统的单向信息发布，系统集成了“求职论坛”和“在线客服”模块，增强了用户之间的横向交流以及用户与平台之间的纵向沟通，提升了平台的活跃度与服务响应速度。</li>
<li><strong>细粒度的数据追踪</strong>：通过“我的收藏”和“我的发布”模块，系统能够帮助用户沉淀有价值的信息资产，同时后台可通过这些数据了解用户偏好，为潜在的个性化推荐打下数据基础。</li>
</ol>
<h2>部署环境</h2>
<p>为确保“简历系统”正常运行，需准备以下软件环境：</p>
<ul>
<li><strong>操作系统</strong>：Windows 7/10/11, Linux (CentOS/Ubuntu), macOS。</li>
<li><strong>Java 运行环境</strong>：JDK 1.8 及以上版本（建议 JDK 1.8_202+）。</li>
<li><strong>数据库</strong>：MySQL 5.7 或 MySQL 8.0 及以上版本。</li>
<li><strong>构建工具</strong>：Maven 3.6+ （用于后端依赖管理）；Node.js 12+ 及 npm/yarn （用于前端 Vue 项目编译，若为打包后部署则仅需静态服务器）。</li>
<li><strong>Web 服务器</strong>：内置 Tomcat (由 Spring Boot Starter Web 提供)，生产环境可选 Nginx 作为反向代理。</li>
<li><strong>开发工具</strong>：IntelliJ IDEA 或 Eclipse (后端开发)，VS Code (前端开发)。</li>
</ul>
<h2>五、技术特性</h2>
<ul>
<li>前后端集成部署，前端资源打包至后端 static 目录</li>
<li>使用 MyBatis-Plus 简化数据访问层开发</li>
<li>集成 Shiro 权限框架实现角色权限控制</li>
</ul>
<h2>六、功能模块截图</h2>
<h3>前台用户端</h3>
<h4>前台登录页</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/02.jpg" alt="前台登录页"></a></p>
<h4>前台注册页</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/03.jpg" alt="前台注册页"></a></p>
<h4>前台-求职论坛列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/04.jpg" alt="前台-求职论坛列表"></a></p>
<h4>前台-系统公告列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/05.jpg" alt="前台-系统公告列表"></a></p>
<h4>前台首页</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/06.jpg" alt="前台首页"></a></p>
<h4>前台个人中心</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/07.jpg" alt="前台个人中心"></a></p>
<h4>前台-简历模板列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/08.jpg" alt="前台-简历模板列表"></a></p>
<h4>前台-简历上传列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/09.jpg" alt="前台-简历上传列表"></a></p>
<h4>前台-我的收藏列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/10.jpg" alt="前台-我的收藏列表"></a></p>
<h4>前台-招聘会列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/11.jpg" alt="前台-招聘会列表"></a></p>
<h4>前台-求职论坛-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/12.jpg" alt="前台-求职论坛-详情"></a></p>
<h4>前台-简历模板-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/13.jpg" alt="前台-简历模板-详情"></a></p>
<h4>前台-简历上传-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/14.jpg" alt="前台-简历上传-详情"></a></p>
<h4>前台-系统公告-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/15.jpg" alt="前台-系统公告-详情"></a></p>
<h4>前台-招聘会-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/16.jpg" alt="前台-招聘会-详情"></a></p>
<h4>前台-报名招聘列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/17.jpg" alt="前台-报名招聘列表"></a></p>
<h4>前台-模板类型列表</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/18.jpg" alt="前台-模板类型列表"></a></p>
<h4>前台-报名招聘-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/19.jpg" alt="前台-报名招聘-详情"></a></p>
<h4>前台-模板类型-详情</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/20.jpg" alt="前台-模板类型-详情"></a></p>
<h4>前台-在线客服</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/21.jpg" alt="前台-在线客服"></a></p>
<h3>后台管理端</h3>
<h4>后台-报名招聘</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/22.jpg" alt="后台-报名招聘"></a></p>
<h4>后台-在线客服</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/23.jpg" alt="后台-在线客服"></a></p>
<h4>后台-系统配置</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/24.jpg" alt="后台-系统配置"></a></p>
<h4>后台-论坛</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/25.jpg" alt="后台-论坛"></a></p>
<h4>后台首页</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/26.jpg" alt="后台首页"></a></p>
<h4>后台-简历模板</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/27.jpg" alt="后台-简历模板"></a></p>
<h4>后台-简历上传</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/28.jpg" alt="后台-简历上传"></a></p>
<h4>后台-登录</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/29.jpg" alt="后台-登录"></a></p>
<h4>后台-模板类型</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/30.jpg" alt="后台-模板类型"></a></p>
<h4>后台-公告信息</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/31.jpg" alt="后台-公告信息"></a></p>
<h4>后台-收藏</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/32.jpg" alt="后台-收藏"></a></p>
<h4>后台-招聘会</h4>
<p><a href="https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github" title="查看完整源码"><img src="images/33.jpg" alt="后台-招聘会"></a></p>

---

## 获取完整源码

| 项目 | 说明 |
| --- | --- |
| 项目名 | 简历系统 |
| 运行截图 | 本文 33 张（站点带水印原图，仓库 `images/` 目录） |
| 完整源码 | [https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github](https://geekcode.top/archives/%E7%AE%80%E5%8E%86%E7%B3%BB%E7%BB%9F?utm_source=github) |
| 咨询微信 | **ir9372**（备注：jingpin-yuanma） |
| 更多项目 | [极客代码 geekcode.top](https://geekcode.top/?utm_source=github) |

> 需要源码、部署、改配置、跑不起来等问题，加微信 ir9372 沟通，说明项目名即可。
