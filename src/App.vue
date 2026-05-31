<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const scale = ref(1)

const updateScale = () => {
  const padding = 78
  scale.value = Math.min(
    (window.innerWidth - padding) / 1840,
    (window.innerHeight - padding) / 1030,
    1,
  )
}

onMounted(() => {
  updateScale()
  window.addEventListener('resize', updateScale)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateScale)
})

const categories = [
  { name: '设备A', value: 11502, percent: 16.8, color: '#25b7ff' },
  { name: '设备B', value: 11502, percent: 16.8, color: '#bfe7ff' },
  { name: '设备C', value: 11502, percent: 16.8, color: '#ffd748' },
  { name: '设备D', value: 11502, percent: 16.8, color: '#ff8a80' },
  { name: '设备E', value: 11502, percent: 16.8, color: '#76e2f4' },
].map((item, index) => {
  const angle = 30 + index * 70

  return {
    ...item,
    style: {
      '--angle': `${angle}deg`,
      '--counter-angle': `${82 - angle}deg`,
      '--note-color': item.color,
    },
  }
})

const monthlyAccess = [17, 8, 12, 17, 22, 17, 20, 11, 17, 15, 19, 21]
const receiveBars = [1650, 650, 2250, 2000, 1680, 2350, 1250]
const downloadBars = [760, 360, 1320, 1750, 740, 1350, 760]

const statusCards = [
  { icon: '▰', value: '5243', label: '设备总量', color: 'cyan' },
  { icon: '✖', value: '845', label: '离线设备', color: 'red' },
  { icon: '✓', value: '1052', label: '在线设备', color: 'cyan' },
  { icon: '!', value: '53', label: '异常设备', color: 'yellow' },
]

const navItems = [
  { icon: '☀', label: '环境监测' },
  { icon: '⚙', label: '安全生产' },
  { icon: '▣', label: '智能车间' },
  { icon: '⌂', label: '智能仓储' },
  { icon: '▰', label: '智能运输' },
]

const eventList = Array.from({ length: 3 }, (_, index) => ({
  id: index + 1,
  text: '这是一段事件描述这是一段事件描述这是一段事件描述这是一段事件描述',
  time: '2023-12-28 15:26:18',
}))

const menuLeft = ['总览', '192安全卫士', '智慧水务', '智慧工业', '智慧校园']
const menuRight = ['智慧医疗', '智慧社区', '智慧农业', '环境治理', '进入管理平台']

const particles = Array.from({ length: 72 }, (_, index) => {
  const seed = index + 1
  return {
    id: seed,
    style: {
      '--x': `${(seed * 37) % 100}%`,
      '--y': `${(seed * 53) % 100}%`,
      '--size': `${2 + (seed % 4)}px`,
      '--duration': `${7 + (seed % 9) * 0.8}s`,
      '--blink': `${2 + (seed % 5) * 0.4}s`,
      '--delay': `${seed * -0.17}s`,
    },
  }
})

const comets = Array.from({ length: 8 }, (_, index) => {
  const seed = index + 1
  return {
    id: seed,
    style: {
      '--x': `${(seed * 11) % 82}%`,
      '--y': `${(seed * 19) % 76}%`,
      '--duration': `${6 + seed * 0.9}s`,
      '--delay': `${seed * -1.2}s`,
    },
  }
})

const pillars = Array.from({ length: 28 }, (_, index) => {
  const seed = index + 1
  return {
    id: seed,
    style: {
      '--x': `${7 + seed * 3.1}%`,
      '--y': `${20 + (seed % 8) * 7}%`,
      '--height': `${30 + (seed % 5) * 18}px`,
      '--duration': `${1.8 + (seed % 4) * 0.2}s`,
      '--delay': `${seed * -0.08}s`,
    },
  }
})
</script>

<template>
  <main class="screen">
    <section class="dashboard" :style="{ transform: `scale(${scale})` }">
      <div class="particle-field" aria-hidden="true">
        <span v-for="item in particles" :key="`particle-${item.id}`" class="particle" :style="item.style"></span>
        <i v-for="item in comets" :key="`comet-${item.id}`" class="comet" :style="item.style"></i>
        <b class="scan-beam"></b>
      </div>
      <header class="topbar">
        <nav class="topnav">
          <span v-for="item in menuLeft" :key="item" class="nav-tab">{{ item }}</span>
        </nav>
        <div class="title-box">
          <span class="title-wing"></span>
          <h1>大数据分析平台</h1>
          <span class="title-wing right"></span>
        </div>
        <nav class="topnav right-nav">
          <span v-for="item in menuRight" :key="item" class="nav-tab" :class="{ active: item === '智慧社区' }">
            {{ item }}
          </span>
        </nav>
        <div class="user-line">欢迎登录 <b>admin</b></div>
        <div class="weather-line">☀ 气温 24°C　2023年12月29日 18:20:28</div>
      </header>

      <div class="content-grid">
        <aside class="left-column">
          <section class="panel category-panel">
            <h2>设备分类</h2>
            <div class="donut-wrap">
              <svg class="donut" viewBox="0 0 220 220" aria-label="设备分类环图">
                <circle class="donut-track" cx="110" cy="110" r="78" />
                <g class="donut-ring">
                  <circle
                    v-for="(item, index) in categories"
                    :key="item.name"
                    class="donut-segment"
                    cx="110"
                    cy="110"
                    r="78"
                    :stroke="item.color"
                    :stroke-dasharray="`${item.percent * 4.9} ${490 - item.percent * 4.9}`"
                    :stroke-dashoffset="-index * 96"
                  />
                </g>
                <circle class="donut-inner" cx="110" cy="110" r="56" />
              </svg>
              <div class="donut-center">
                <strong>102,860</strong>
                <span>设备总数</span>
              </div>
              <div class="donut-orbit" aria-hidden="true">
                <div
                  v-for="item in categories"
                  :key="`${item.name}-label`"
                  class="donut-note"
                  :style="item.style"
                >
                  <div class="donut-note-content">
                    <span>{{ item.name }}：{{ item.percent }}%</span>
                    <b>{{ item.value }}</b>
                  </div>
                </div>
              </div>
            </div>
          </section>

          <section class="panel trend-panel">
            <h2>设备接入趋势</h2>
            <div class="chart-label">单位(万个)</div>
            <div class="bar-chart month-chart">
              <div v-for="(value, index) in monthlyAccess" :key="index" class="bar-cell">
                <span class="single-bar" :style="{ height: `${value * 7}px` }"></span>
                <em>{{ index + 1 }}月</em>
              </div>
            </div>
          </section>

          <section class="panel status-panel">
            <h2>设备状态</h2>
            <div class="status-grid">
              <div v-for="item in statusCards" :key="item.label" class="status-item">
                <span class="status-icon" :class="item.color">{{ item.icon }}</span>
                <div>
                  <strong>{{ item.value }}</strong>
                  <p>{{ item.label }}</p>
                </div>
              </div>
            </div>
          </section>
        </aside>

        <section class="center-stage">
          <div class="city-scene">
            <div class="scan-grid"></div>
            <div v-for="item in pillars" :key="item.id" class="data-pillar" :style="item.style"></div>
            <div class="campus">
              <div class="building block-a"></div>
              <div class="building block-b"></div>
              <div class="building block-c"></div>
              <div class="building block-d"></div>
              <div class="building tower"></div>
              <div class="stadium">
                <span></span>
              </div>
              <div class="road main-road"></div>
              <div class="road side-road"></div>
            </div>
          </div>

          <section class="panel quick-panel">
            <h2>快速导航</h2>
            <div class="quick-nav">
              <button v-for="item in navItems" :key="item.label" type="button" class="hex-button">
                <span class="hex-icon">{{ item.icon }}</span>
                <b>{{ item.label }}</b>
              </button>
            </div>
          </section>
        </section>

        <aside class="right-column">
          <section class="panel data-panel">
            <h2>设备数据</h2>
            <div class="mini-title">设备收发数据</div>
            <div class="metric-row">
              <article class="metric green">
                <span>◰</span>
                <strong>555,621</strong>
                <p>今日接收数据</p>
              </article>
              <article class="metric yellow">
                <span>↧</span>
                <strong>125,023</strong>
                <p>今日下发数据</p>
              </article>
            </div>
            <div class="legend"><span class="blue"></span>接收量 <span class="gold"></span>下发量</div>
            <div class="bar-chart double-chart">
              <div v-for="(value, index) in receiveBars" :key="index" class="bar-cell double">
                <span class="single-bar blue" :style="{ height: `${value / 14}px` }"></span>
                <span class="single-bar gold" :style="{ height: `${downloadBars[index] / 14}px` }"></span>
                <em>12/{{ 25 + index }}</em>
              </div>
            </div>
            <div class="mini-title warning-title">设备告警数据</div>
            <div class="metric-row">
              <article class="metric red">
                <span>☀</span>
                <strong>1,621</strong>
                <p>今日告警数量</p>
              </article>
              <article class="metric mint">
                <span>☀</span>
                <strong>865</strong>
                <p>今日已解除告警</p>
              </article>
            </div>
          </section>

          <section class="panel event-panel">
            <h2>大事记</h2>
            <article v-for="item in eventList" :key="item.id" class="event-card">
              <span class="event-icon">▤</span>
              <div>
                <p>{{ item.text }}</p>
                <time>{{ item.time }}</time>
              </div>
              <button type="button">查看详情 ›</button>
            </article>
          </section>
        </aside>
      </div>
    </section>
  </main>
</template>
