# 项目长期记忆 · 宏观事件日历 / 重要信息源导航

## 项目形态
- 交付物是**两份单文件静态 HTML**，零依赖、数据内嵌 JS 数组，微信可直接打开：
  - `宏观事件日历_对外版.html`（对外分享）
  - `重要信息源导航_内部维护版.html`（带来源徽章与维护弹层）
- **两份的数据数组必须同步**：`CPI_ROWS` / `PPI_ROWS` / `PMI_ROWS` / `CAL_EVENTS` / `CAL_NOTES` / `ARCHIVE`。

## 用户偏好与硬性约定
- 每行只保留**一个**「数据 ↗」直达链接指向官方原文；**不要恢复**「查询」按钮与二级站点选择弹层。
- 板块固定四块：CPI、PPI、PMI、新闻联播；三个指数**只做中国**，美国部分已整体删除。
- 明确**不做**：走势折线图与悬浮明细（P2）、顶部导航加「当前基调」锚点。
- 页面时间用 `TODAY` 变量运行时计算，不写死日期。

## 数据源踩坑（反复用到）
- `bls.gov` 对中国大陆 IP 地理封锁，新闻稿/归档/download 全 403 → 美国数据改用东方财富 / 金十数据中心。
- `data.stats.gov.cn/easyquery.htm` 是 URL 级 WAF 拦截（`reason:UrlACL`），任何 IP 都打不开，别再放进页面。
- 年度数据用各年《国民经济和社会发展统计公报》原文，每年一个独立 URL。
- 月度稿真实 URL 靠翻统计局「最新发布」列表页分页（`index.html` / `index_1.html` … `index_9.html`）取得；按月归档目录 `sj/zxfb/YYYYMM/` 直连 403。
- 2026 年稿子统一路径 `sj/zxfb/YYYYMM/tYYYYMMDD_XXXXXXX.html`。

## 发布与存放
- 线上站点（地址长期不变，重新发布即更新）：`https://macro-event-calendar.app.workbuddy.host/`
- 资料库个人空间根目录三个节点：
  - 对外版页面 `d2QOkjjxvFNP1N8cRkrKqO`
  - 内部版页面 `2SjjyG6Dsm1K2LozSEi2VH`
  - 跨设备交接文档 `B3w4tL7qffP9lK5lSIxByZ`
- **资料库会给 HTML 每个元素加 `data-page-node-id` 埋点并注入 `page_comm/inject.js`**（体积 110KB→146KB），
  所以不能用 MD5 判断云端是否最新，要 diff 内容。

## Git / 跨设备
- 本地已 `git init -b main`（2026-10-16），私有仓库，远端 GitHub + Gitee 双份。
- GitHub 账号 `corlong`，SSH 已授权；Gitee 公钥待用户添加。
- `.gitignore` 排除 `.wbapp_*.genie`、`.workbuddy/applications.yaml`；`.workbuddy/memory` **刻意入库**，
  因为本地记忆不会跨设备同步，入库后新机器才能接着干。
- 私有仓库开不了免费 GitHub Pages，在线链接仍走上面的部署站点。
