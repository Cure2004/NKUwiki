<script setup lang="ts">
import { withBase } from 'vitepress'
import HoverMedia from './HoverMedia.vue'

// 本站内的图片路径（/img/...）统一经 withBase 拼接 base；外部链接原样保留。
const links = [
	{ name: '南开大学', image: '/img/10/10/南开大学WX头像.jpg', url: 'http://weixin.qq.com/r/mp/-3VFXTHEM2xMrXU_9yDt', description: '允公允能，日新月异。这里是南开大学官微，百年南开欢迎你~', tag: '校园媒体', qr: true },
	{ name: 'NKUwiki项目组', image: '/img/10/10/NKUwiki项目组QQ头像.svg', url: '/img/10/10/NKUwiki项目组QQ.jpg', description: 'NKUwiki项目组', tag: '项目群组', preview: true },
	{ name: 'NCEPUwiki', image: '/img/10/10/NCEPUwiki头像.svg', url: 'https://wiki.ncepuinfo.cc/', description: '华北电力大学学生共同维护的非官方校园知识库', tag: '兄弟院校' },
].map(link => ({ ...link, image: withBase(link.image), url: link.url.startsWith('/') ? withBase(link.url) : link.url }))
</script>

<template>
<p class="friend-intro">
	连接创作者、社区与知识库。
</p>
<div class="friend-list">
	<article v-for="link in links" :key="link.name" class="friend-link-card">
		<img class="card-blur" :src="link.image" alt="" loading="lazy">
		<component :is="link.qr || link.preview ? 'div' : 'a'" class="friend-card-main" :href="link.qr || link.preview ? undefined : link.url" :target="link.qr || link.preview ? undefined : '_blank'" rel="noreferrer">
			<img class="card-avatar" :src="link.image" :alt="link.name" loading="lazy">
			<h2>{{ link.name }}</h2>
			<p>{{ link.description }}</p>
			<span class="card-badges">{{ link.tag }}</span>
			<HoverMedia v-if="link.qr || link.preview" :src="link.url" :kind="link.qr ? 'qr' : 'image'" :label="link.qr ? '微信扫码关注' : `查看${link.name}图片`" /><span v-else class="friend-card-visit">访问 ↗</span>
		</component>
	</article>
</div>
</template>
