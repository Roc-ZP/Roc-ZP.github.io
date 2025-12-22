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
    </header>
    
    <main>
      <!-- 文章卡片 -->
      <a 
        href="#" 
        class="article-link" 
        v-for="(article, index) in articles" 
        :key="index"
        @click.prevent="showArticleInfo(index)"
      >
        <article>
          <h2>{{ article.title }}</h2>
          <p class="date">发布日期：{{ article.date }}</p>
          <div v-for="(paragraph, pIndex) in article.content" :key="pIndex">
            <p>{{ paragraph }}</p>
          </div>
          <ul v-if="article.list && article.list.length > 0">
            <li v-for="(item, i) in article.list" :key="i">{{ item }}</li>
          </ul>
          <p v-if="article.note" class="note">{{ article.note }}</p>
        </article>
      </a>
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
      ]
    }
  },
  mounted() {
    // 初始化主题
    this.initTheme();
    
    // 添加键盘快捷键支持
    document.addEventListener('keydown', this.handleKeyDown);
  },
  beforeUnmount() {
    // 清理事件监听器
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
  --article-bg: white;
  --border-color: #eaeaea;
  --accent-color: #3498db;
  --footer-color: #7f8c8d;
  --shadow-color: rgba(0,0,0,0.1);
  --toggle-bg: #f0f0f0;
  --toggle-color: #666;
}

/* 深色模式颜色变量 */
.dark-mode {
  --bg-color: #0d1117;
  --text-color: #c9d1d9;
  --header-color: #ffffff;
  --article-bg: #161b22;
  --border-color: #30363d;
  --accent-color: #58a6ff;
  --footer-color: #8b949e;
  --shadow-color: rgba(0,0,0,0.4);
  --toggle-bg: #21262d;
  --toggle-color: #c9d1d9;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
  line-height: 1.6;
  color: var(--text-color);
  background-color: var(--bg-color);
  min-height: 100vh;
}

.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

header {
  text-align: center;
  padding: 40px 0;
  border-bottom: 1px solid var(--border-color);
  margin-bottom: 40px;
  position: relative;
}

header h1 {
  color: var(--header-color);
  margin-bottom: 10px;
  font-size: 2.5em;
}

.tagline {
  color: var(--footer-color);
  font-size: 1.2em;
  font-weight: 300;
}

article {
  background: var(--article-bg);
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 4px 20px var(--shadow-color);
  margin-bottom: 30px;
  border: 1px solid var(--border-color);
}

h2 {
  color: var(--accent-color);
  margin-bottom: 15px;
  font-size: 1.8em;
}

.date {
  color: var(--footer-color);
  font-size: 0.9em;
  margin-bottom: 20px;
  display: flex;
  align-items: center;
  gap: 8px;
}

.date::before {
  content: "📅";
}

footer {
  text-align: center;
  margin-top: 50px;
  padding-top: 20px;
  border-top: 1px solid var(--border-color);
  color: var(--footer-color);
  font-size: 0.9em;
}

a {
  color: var(--accent-color);
  text-decoration: none;
  font-weight: 500;
}

a:hover {
  text-decoration: underline;
  opacity: 0.8;
}

ul {
  margin-left: 20px;
  margin-top: 15px;
  margin-bottom: 10px;
}

li {
  margin-bottom: 8px;
  padding-left: 10px;
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
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  display: flex;
  align-items: center;
  gap: 8px;
  z-index: 1000;
  box-shadow: 0 2px 8px var(--shadow-color);
}

.theme-toggle:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px var(--shadow-color);
}

.theme-toggle:active {
  transform: translateY(0);
}

/* 文章卡片链接样式 */
.article-link {
  text-decoration: none;
  color: inherit;
  display: block;
  margin-bottom: 30px;
}

.article-link article {
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
}

.article-link:hover article {
  transform: translateY(-5px);
  box-shadow: 0 8px 25px var(--shadow-color);
}

.article-link:active article {
  transform: translateY(-2px);
}

/* 猫爪元素装饰 */
.cat-paw {
  position: fixed;
  opacity: 0.1;
  z-index: -1;
  font-size: 40px;
}

.dark-mode .cat-paw {
  opacity: 0.05;
}

.note {
  margin-top: 15px;
  color: var(--accent-color);
  font-style: italic;
}

/* 响应式设计 */
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
  
  article {
    padding: 20px;
  }
}
</style>