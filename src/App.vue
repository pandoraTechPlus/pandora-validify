<template>
  <rapi-doc
    spec-url="/openapi.json"
    :render-style="renderStyle"
    show-header="true"
    allow-spec-file-load="false"
    allow-server-selection="false"
    allow-spec-url-load="false"
    theme="light"
    nav-logo="/pandora.jpg"
    allow-authentication="false"
    heading-text="Validify API Docs"
    style="width: 100vw; height: 100vh; padding: 0; margin: 0"
  ></rapi-doc>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const renderStyle = ref('read') // default for large screens

const updateRenderStyle = () => {
  renderStyle.value = window.innerWidth < 768 ? 'view' : 'read'
}

onMounted(() => {
  const script = document.createElement('script')
  script.src = 'https://unpkg.com/rapidoc/dist/rapidoc-min.js'
  document.body.appendChild(script)

  updateRenderStyle()
  window.addEventListener('resize', updateRenderStyle)
})

onBeforeUnmount(() => {
  window.removeEventListener('resize', updateRenderStyle)
})
</script>

<style>
html,
body {
  margin: 0;
  padding: 0;
  width: 100vw;
  height: 100vh;
  overflow: hidden;
}
</style>
