<template>
  <div class="container">
    <!-- 装饰性猫爪 -->
    <div class="cat-paw" style="top: 10%; left: 10%;">🐾</div>
    <div class="cat-paw" style="bottom: 20%; right: 15%;">🐾</div>
    
    <!-- 深色模式切换按钮 -->
    <button id="themeToggle" class="theme-toggle" @click="toggleTheme">
      <span id="themeIcon">{{ isDarkMode ? '☀️' : '🌙' }}</span>
      <span id="themeText">{{ isDarkMode ? '浅色模式' : '深色模式' }}</span>
    </button>
    
    <header>
      <h1>萝卜之家</h1>
      <p class="tagline">记录生活，分享傻猫</p>
      <!-- 添加导航菜单 -->
      <nav class="navigation">
        <a href="#" @click.prevent="currentView = 'home'" :class="{ active: currentView === 'home' }">首页</a>
        <a href="#" @click.prevent="currentView = 'bookmarks'" :class="{ active: currentView === 'bookmarks' }">个人收藏网址</a>
      </nav>
    </header>
    
    <main>
      <!-- 首页内容 -->
      <div v-if="currentView === 'home'" class="home-content">
        <div class="welcome-section">
          <h2>欢迎回来！</h2>
          <p class="welcome-text">今天是 {{ currentDate }}</p>
        </div>
        
        <!-- 文章卡片 -->
        <div class="articles-grid">
          <div 
            class="article-card"
            v-for="(article, index) in articles" 
            :key="index"
            @click="showArticleInfo(index)"
          >
            <div class="article-header">
              <h3>{{ article.title }}</h3>
              <span class="article-date">📅 {{ article.date }}</span>
            </div>
            <div class="article-content">
              <div v-for="(paragraph, pIndex) in article.content" :key="pIndex">
                <p>{{ paragraph }}</p>
              </div>
              <ul v-if="article.list && article.list.length > 0">
                <li v-for="(item, i) in article.list" :key="i">{{ item }}</li>
              </ul>
              <p v-if="article.note" class="note">{{ article.note }}</p>
            </div>
          </div>
        </div>
      </div>

      <!-- 收藏网址内容 -->
      <div v-if="currentView === 'bookmarks'" class="bookmarks-content">
        <div class="bookmarks-header">
          <h2>🐱 个人收藏网址</h2>
          <p class="section-description">我经常访问的有用网站</p>
        </div>
        
        <!-- 收藏网址网格布局 -->
        <div class="bookmarks-grid">
          <!-- 技术类网站 -->
          <div class="bookmark-category-card">
            <h3 class="category-title">💻 技术学习</h3>
            <div class="category-bookmarks">
              <a v-for="bookmark in techBookmarks" :key="bookmark.name" 
                 :href="bookmark.url" target="_blank" class="bookmark-item">
                <div class="bookmark-icon">🔗</div>
                <div class="bookmark-content">
                  <h4>{{ bookmark.name }}</h4>
                  <p>{{ bookmark.description }}</p>
                </div>
              </a>
            </div>
          </div>
          
          <!-- 工具类网站 -->
          <div class="bookmark-category-card">
            <h3 class="category-title">🛠️ 实用工具</h3>
            <div class="category-bookmarks">
              <a v-for="bookmark in toolBookmarks" :key="bookmark.name" 
                 :href="bookmark.url" target="_blank" class="bookmark-item">
                <div class="bookmark-icon">🔧</div>
                <div class="bookmark-content">
                  <h4>{{ bookmark.name }}</h4>
                  <p>{{ bookmark.description }}</p>
                </div>
              </a>
            </div>
          </div>
          
          <!-- 娱乐类网站 -->
          <div class="bookmark-category-card">
            <h3 class="category-title">🎮 娱乐休闲</h3>
            <div class="category-bookmarks">
              <a v-for="bookmark in entertainmentBookmarks" :key="bookmark.name" 
                 :href="bookmark.url" target="_blank" class="bookmark-item">
                <div class="bookmark-icon">🎬</div>
                <div class="bookmark-content">
                  <h4>{{ bookmark.name }}</h4>
                  <p>{{ bookmark.description }}</p>
                </div>
              </a>
            </div>
          </div>
        </div>
      </div>
    </main>
    
    <footer>
      <p>© 2025 萝卜之家 | 由 <a href="https://pages.github.com/" target="_blank">GitHub Pages</a> 驱动</p>
      <p>联系方式：563692928@qq.com | 主题切换已启用</p>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isDarkMode: false,
      currentView: 'home',
      currentDate: new Date().toLocaleDateString('zh-CN', { 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric',
        weekday: 'long'
      }),
      articles: [
        {
          title: '欢迎来到萝卜之家！',
          date: '2025年12月',
          content: [
            '这是我的第一篇博客文章，主要是想做个博客，记录一下生活。',
            '除了记录生活，各种乱七八糟的东西我都会记录、学习一下，想在这个互联网时代留下一些痕迹。',
            '👆 点击右上角按钮可以切换深色/浅色模式'
          ],
          note: ''
        },
        {
          title: '关于萝卜之家',
          date: '2025年12月',
          content: [
            '这个博客使用纯HTML/CSS构建（其实就是问ai搞的模板哈哈），部署在GitHub Pages上（免费！顺便学习一下git怎么用）。',
            '未来我会在这里分享：'
          ],
          list: [
            '技术学习心得',
            '项目开发经验',
            '读书笔记',
            '生活感悟',
            '傻猫日常'
          ],
          note: '💡 提示：你的主题偏好会被自动保存'
        }
      ],
      techBookmarks: [
        {
          name: 'MDN Web Docs',
          url: 'https://developer.mozilla.org',
          description: 'Web开发技术文档'
        },
        {
          name: 'Vue.js 官网',
          url: 'https://vuejs.org',
          description: 'Vue.js 框架官方文档'
        },
        {
          name: 'GitHub',
          url: 'https://github.com',
          description: '代码托管平台'
        }
      ],
      toolBookmarks: [
        {
          name: 'Can I Use',
          url: 'https://caniuse.com',
          description: '浏览器兼容性查询'
        },
        {
          name: 'Figma',
          url: 'https://figma.com',
          description: '在线设计工具'
        },
        {
          name: 'CodePen',
          url: 'https://codepen.io',
          description: '在线代码编辑器'
        }
      ],
      entertainmentBookmarks: [
        {
          name: 'Bilibili',
          url: 'https://bilibili.com',
          description: '大龄儿童乐园'
        },
        {
          name: '知乎',
          url: 'https://zhihu.com',
          description: '赛博故事会'
        }
      ]
    }
  },
  mounted() {
    this.initTheme();
    document.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    document.removeEventListener('keydown', this.handleKeyDown);
  },
  methods: {
    toggleTheme() {
      this.isDarkMode = !this.isDarkMode;
      document.body.classList.toggle('dark-mode', this.isDarkMode);
      localStorage.setItem('theme', this.isDarkMode ? 'dark' : 'light');
    },
    initTheme() {
      const savedTheme = localStorage.getItem('theme');
      const systemPrefersDark = window.matchMedia('(prefers-color-scheme: dark)').matches;
      
      if (savedTheme) {
        this.isDarkMode = savedTheme === 'dark';
      } else {
        this.isDarkMode = systemPrefersDark;
      }
      
      if (this.isDarkMode) {
        document.body.classList.add('dark-mode');
      }
    },
    handleKeyDown(e) {
      if (e.key === 't' || e.key === 'T') {
        this.toggleTheme();
      }
    },
    showArticleInfo(index) {
      if (index === 0) {
        alert('欢迎来到萝卜之家！\n\n这篇文章介绍了网站的基本情况。\n\n更多内容敬请期待！');
      } else {
        alert('关于萝卜之家\n\n这里会介绍网站的功能和未来计划。\n\n更多内容敬请期待！');
      }
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  transition: background-color 0.3s, color 0.3s, border-color 0.3s, box-shadow 0.3s;
}

/* 颜色变量定义 */
:root {
  --bg-color: #f8f9fa;
  --text-color: #333;
  --header-color: #2c3e50;
  --card-bg: white;
  --border-color: #eaeaea;
  --accent-color: #3498db;
  --footer-color: #7f8c8d;
  --shadow-color: rgba(0,0,0,0.1);
  --toggle-bg: #f0f0f0;
  --toggle-color: #666;
  --grid-bg: #f1f3f4;
}

/* 深色模式颜色变量 */
.dark-mode {
  --bg-color: #0d1117;
  --text-color: #c9d1d9;
  --header-color: #ffffff;
  --card-bg: #161b22;
  --border-color: #30363d;
  --accent-color: #58a6ff;
  --footer-color: #8b949e;
  --shadow-color: rgba(0,0,0,0.4);
  --toggle-bg: #21262d;
  --toggle-color: #c9d1d9;
  --grid-bg: #0d1117;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--bg-color);
  min-height: 100vh;
  background-image: 
    radial-gradient(circle at 10% 20%, rgba(52, 152, 219, 0.05) 0%, transparent 20%),
    radial-gradient(circle at 90% 80%, rgba(52, 152, 219, 0.05) 0%, transparent 20%);
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

/* 头部样式 */
header {
  text-align: center;
  padding: 40px 0 20px;
  margin-bottom: 30px;
  position: relative;
}

header h1 {
  color: var(--header-color);
  margin-bottom: 10px;
  font-size: 2.5em;
  font-weight: 600;
}

.tagline {
  color: var(--footer-color);
  font-size: 1.2em;
  font-weight: 300;
  margin-bottom: 20px;
}

/* 导航菜单样式 */
.navigation {
  margin-top: 20px;
  display: flex;
  gap: 20px;
  justify-content: center;
}

.navigation a {
  padding: 10px 20px;
  border-radius: 25px;
  background: var(--grid-bg);
  color: var(--text-color);
  text-decoration: none;
  font-weight: 500;
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
}

.navigation a:hover {
  background: var(--accent-color);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px var(--shadow-color);
}

.navigation a.active {
  background: var(--accent-color);
  color: white;
  border-color: var(--accent-color);
}

/* 主要内容区域 */
main {
  flex: 1;
  margin-bottom: 30px;
}

/* 首页内容样式 */
.home-content {
  padding: 0 20px;
}

.welcome-section {
  text-align: center;
  margin-bottom: 40px;
  padding: 20px;
  background: var(--grid-bg);
  border-radius: 12px;
  border: 1px solid var(--border-color);
}

.welcome-section h2 {
  color: var(--accent-color);
  font-size: 2em;
  margin-bottom: 10px;
}

.welcome-text {
  color: var(--footer-color);
  font-size: 1.1em;
}

.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
  gap: 25px;
  margin-top: 20px;
}

.article-card {
  background: var(--card-bg);
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 4px 20px var(--shadow-color);
  border: 1px solid var(--border-color);
  text-align: left;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
}

.article-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--accent-color);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.article-card:hover::before {
  transform: scaleX(1);
}

.article-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px var(--shadow-color);
}

.article-header {
  margin-bottom: 15px;
  padding-bottom: 10px;
  border-bottom: 1px solid var(--border-color);
}

.article-header h3 {
  color: var(--accent-color);
  margin-bottom: 5px;
  font-size: 1.4em;
}

.article-date {
  color: var(--footer-color);
  font-size: 0.9em;
}

.article-content p {
  margin-bottom: 10px;
  line-height: 1.6;
}

.article-content ul {
  margin-left: 20px;
  margin-top: 10px;
  margin-bottom: 10px;
}

.article-content li {
  margin-bottom: 8px;
  padding-left: 5px;
}

.note {
  margin-top: 15px;
  color: var(--accent-color);
  font-style: italic;
  padding: 10px;
  background: rgba(52, 152, 219, 0.1);
  border-radius: 6px;
  border-left: 3px solid var(--accent-color);
}

/* 收藏网址内容样式 */
.bookmarks-content {
  padding: 0 20px;
}

.bookmarks-header {
  text-align: center;
  margin-bottom: 40px;
}

.bookmarks-header h2 {
  color: var(--accent-color);
  margin-bottom: 10px;
  font-size: 2em;
}

.section-description {
  color: var(--footer-color);
  margin-bottom: 30px;
  font-size: 1.1em;
}

/* 收藏网址网格布局 - 已修改为3列横向布局 */
.bookmarks-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr); /* 改为固定3列，实现横向布局 */
  gap: 25px;
  margin-top: 20px;
}

.bookmark-category-card {
  background: var(--card-bg);
  padding: 25px;
  border-radius: 12px;
  box-shadow: 0 4px 20px var(--shadow-color);
  border: 1px solid var(--border-color);
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  height: 100%; /* 使所有卡片高度一致 */
}

.bookmark-category-card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: var(--accent-color);
  transform: scaleX(0);
  transition: transform 0.3s ease;
}

.bookmark-category-card:hover::before {
  transform: scaleX(1);
}

.bookmark-category-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px var(--shadow-color);
}

.category-title {
  color: var(--accent-color);
  margin-bottom: 20px;
  font-size: 1.4em;
  display: flex;
  align-items: center;
  gap: 10px;
  padding-bottom: 10px;
  border-bottom: 1px solid var(--border-color);
}

.category-bookmarks {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.bookmark-item {
  display: flex;
  align-items: center;
  padding: 15px;
  border: 1px solid var(--border-color);
  border-radius: 8px;
  text-decoration: none;
  color: var(--text-color);
  transition: all 0.3s ease;
  background: var(--card-bg);
}

.bookmark-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px var(--shadow-color);
  border-color: var(--accent-color);
  background: var(--grid-bg);
}

.bookmark-icon {
  font-size: 24px;
  margin-right: 15px;
  flex-shrink: 0;
}

.bookmark-content h4 {
  color: var(--accent-color);
  margin-bottom: 5px;
  font-size: 1.1em;
}

.bookmark-content p {
  color: var(--footer-color);
  font-size: 0.9em;
  margin: 0;
  line-height: 1.4;
}

/* 深色模式切换按钮 - 更美观 */
.theme-toggle {
  position: fixed;
  top: 20px;
  right: 20px;
  background: var(--toggle-bg);
  color: var(--toggle-color);
  border: 1px solid var(--border-color);
  padding: 10px 15px;
  border-radius: 25px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  display: flex;
  align-items: center;
  gap: 8px;
  z-index: 1000;
  box-shadow: 0 2px 8px var(--shadow-color);
  backdrop-filter: blur(10px);
  transition: all 0.3s ease;
}

.theme-toggle:hover {
  background: var(--accent-color);
  color: white;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px var(--shadow-color);
}

/* 猫爪元素装饰 */
.cat-paw {
  position: fixed;
  opacity: 0.05;
  z-index: -1;
  font-size: 60px;
  pointer-events: none;
  animation: float 6s ease-in-out infinite;
}

.cat-paw:nth-child(2n) {
  animation-delay: -2s;
}

@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-10px) rotate(5deg); }
}

.dark-mode .cat-paw {
  opacity: 0.02;
}

/* 页脚样式 */
footer {
  text-align: center;
  margin-top: 50px;
  padding-top: 20px;
  border-top: 1px solid var(--border-color);
  color: var(--footer-color);
  font-size: 0.9em;
  padding-bottom: 20px;
}

footer a {
  color: var(--accent-color);
  text-decoration: none;
  font-weight: 500;
}

footer a:hover {
  text-decoration: underline;
}

/* 响应式设计 */
@media (max-width: 1024px) {
  .bookmarks-grid {
    grid-template-columns: repeat(2, 1fr); /* 在平板设备上显示2列 */
  }
}

@media (max-width: 768px) {
  .container {
    padding: 15px;
  }
  
  header h1 {
    font-size: 2em;
  }
  
  .theme-toggle {
    position: absolute;
    top: 15px;
    right: 15px;
  }
  
  .articles-grid,
  .bookmarks-grid {
    grid-template-columns: 1fr; /* 手机端改为单列 */
    gap: 20px;
  }
  
  .navigation {
    flex-direction: column;
    align-items: center;
    gap: 10px;
  }
  
  .welcome-section {
    padding: 15px;
  }
  
  .article-card,
  .bookmark-category-card {
    padding: 20px;
  }
}
</style>