<!-- ============================================================
  App.vue —— ch05-routing 第 5 章实验台（路由版）
  上一章的实验台是"锚点菜单"，这一章换成 router-link 导航：
  导航栏 + 唯一出口 <router-view>，地址栏就是实验记录仪。
  注意：router-link/router-view 没有 import、没注册——
  它们是 app.use(router) 之后全局可用的"官方组件"。
============================================================ -->
<template>
  <div id="app">
    <header class="chapter-heading">
      <div class="heading-copy">
        <p class="heading-eyebrow">VUE.JS FRONT-END DEVELOPMENT</p>
        <h1 class="chapter-title"><span>Vue.js 前端开发实战</span><span class="chapter-tag">Ch05</span></h1>
        <p class="chapter-subtitle">第 5 章实验台 · 第 05 课（5.1—5.6）：路由——地址栏变，组件换，页面不刷新</p>
      </div>
      <span class="chapter-number" aria-hidden="true">05</span>
    </header>
    <nav class="top-nav">
      <!-- router-link = 会走路由的 <a>：to 写目标地址（别忘引号）；渲染后自动带高亮类 -->
      <router-link to="/home">首页</router-link>
      <router-link to="/about">关于</router-link>
      <router-link to="/users">用户列表</router-link>      <!-- 补全：地址见任务 3 -->
      <router-link to="/center">用户中心</router-link>      <!-- 补全：地址见任务 4 -->
      <router-link to="/named">命名路由</router-link>      <!-- 补全：地址见任务 5 -->
      <router-link to="/program">编程式导航</router-link>    <!-- 补全：地址见任务 6 -->
      <router-link to="/search">搜索</router-link>          <!-- 补全：地址见任务 6 -->
    </nav>
    <!-- $route.fullPath = 当前完整地址——地址栏的"回声"，实验时盯它 -->
    <div class="status-bar">
      <span class="status-item"><span class="status-dot"></span><b>当前路由</b><code>{{ $route.fullPath }}</code></span>
      <span class="status-divider"></span>
      <span class="status-item">登录态 <b>{{ $route.path === '/login' || isLogin() ? '已登录' : '未登录' }}</b></span>
    </div>
    <!-- 补全：唯一的顶层路由出口组件（一对标签）——地址匹配到谁，谁就显示在这里 -->
    <router-view></router-view>
  </div>
</template>
<script>
export default {
  name: 'App',
  methods: {
    // 用方法不用 computed：localStorage 不是响应式数据，computed 没有响应式依赖会被缓存成"旧值"；
    // 方法每次渲染都重查——路由一变页面重渲染，登录态跟着刷新
    isLogin() {
      return !!localStorage.getItem('token')
    }
  }
}
</script>
<style scoped>
.chapter-heading {
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  min-height: 194px;
  margin: 0 0 24px;
  padding: 30px 40px;
  border: 1px solid rgba(255, 255, 255, 0.22);
  border-radius: 20px;
  background: linear-gradient(112deg, #17684f 0%, #27886a 52%, #67b989 100%);
  color: #fff;
  box-shadow: 0 18px 38px rgba(35, 105, 73, 0.2);
  box-sizing: border-box;
}
.heading-copy {
  position: relative;
  z-index: 1;
}
.heading-eyebrow {
  margin: 0 0 16px;
  color: rgba(255, 255, 255, 0.82);
  font-size: 11px;
  font-weight: 750;
  letter-spacing: 2px;
}
.chapter-title {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 14px;
  margin: 0;
  color: #fff;
  font-size: 38px;
  font-weight: 750;
  line-height: 1.2;
}
.chapter-tag {
  display: inline-flex;
  align-items: center;
  border: 0;
  border-radius: 5px;
  background: transparent;
  color: #fff;
  padding: 3px 0;
  font-family: Consolas, Monaco, monospace;
  font-size: 23px;
  font-weight: 750;
  line-height: 1.2;
}
.chapter-subtitle {
  margin: 14px 0 0;
  color: rgba(255, 255, 255, 0.88);
  font-size: 14px;
}
.chapter-number {
  position: absolute;
  right: 24px;
  bottom: -42px;
  color: rgba(255, 255, 255, 0.13);
  font-size: 180px;
  font-weight: 800;
  line-height: 1;
  user-select: none;
}
.top-nav {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  gap: 4px;
  margin: 0 0 18px;
  padding: 12px 16px;
  border: 1px solid var(--border);
  border-radius: 17px;
  background: var(--card);
  box-shadow: 0 8px 20px rgba(43, 89, 63, 0.06);
}
.top-nav a {
  color: #4b5874;
  text-decoration: none;
  border: 1px solid transparent;
  border-radius: 999px;
  padding: 8px 14px;
  font-size: 13px;
  font-weight: 600;
  transition: background-color 160ms ease, color 160ms ease, box-shadow 160ms ease;
}
.top-nav a:hover {
  background: var(--primary-bg);
  color: var(--primary-dark);
}
/* router-link 匹配当前地址时自动带上 router-link-active 类——白送的高亮 */
.top-nav a.router-link-active {
  background: var(--primary);
  color: #fff;
  box-shadow: 0 5px 12px rgba(29, 103, 79, 0.24);
}
.status-bar {
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
  min-height: 48px;
  margin: 0 0 22px;
  padding: 8px 14px;
  border: 1px solid var(--border);
  border-radius: 12px;
  background: rgba(255, 255, 255, 0.78);
  color: #4b5874;
  box-sizing: border-box;
  font-size: 13px;
}
.status-item {
  display: inline-flex;
  align-items: center;
  gap: 8px;
}
.status-dot {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: #36b58c;
  box-shadow: 0 0 0 4px rgba(54, 181, 140, 0.12);
}
.status-divider {
  width: 1px;
  height: 20px;
  background: var(--border);
}
code {
  background: var(--primary-bg);
  border-radius: 4px;
  padding: 0 6px;
  font-family: Consolas, Monaco, monospace;
}
.muted {
  color: var(--muted);
  margin-top: 0;
}
@media (max-width: 600px) {
  .chapter-heading {
    min-height: 170px;
    padding: 24px;
  }
  .chapter-title {
    gap: 10px;
    font-size: 29px;
  }
  .chapter-subtitle {
    max-width: 34em;
    line-height: 1.6;
  }
  .chapter-number {
    right: 8px;
    bottom: -22px;
    font-size: 120px;
  }
  .top-nav {
    padding: 9px;
    gap: 2px;
  }
  .top-nav a {
    padding: 7px 10px;
  }
  .status-bar {
    gap: 8px;
  }
  .status-divider {
    display: none;
  }
}
</style>
