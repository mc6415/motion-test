<script setup>
import { scroll, animate, ScrollOffset } from 'motion'
import { ref, onMounted } from 'vue'

defineProps({
  msg: String
})

onMounted(() => {
  // get all elements with copy-block class
  const copyBlocks = document.querySelectorAll('.copy-block')
  const container = document.querySelector('section');
  const progressBar = document.querySelector('.progress-bar');

  // animate progress-bar on scroll down page from scalex 0 to 1
  scroll(
    animate(progressBar, { scaleX: [0, 1]}),
  )

  // for each block in copyBlocks console log block
  copyBlocks.forEach(block => {
    const scrollOffsetStart = block.attributes['data-start']?.value;
    const scrollOffsetEnd = block.attributes['data-end']?.value;

    if(scrollOffsetStart && scrollOffsetEnd) {
      let opacityChange = [0, 1, 0];
      if(scrollOffsetStart == 0) {
        opacityChange = [1, 0]
      }

      scroll(
        animate(block, { opacity: opacityChange }), {
        target: container,
        offset: [`${scrollOffsetStart}%`, `${scrollOffsetEnd}%`]
      })
    }
  })

})

const count = ref(0)
</script>

<template>
  <div class="progress-bar" />
  <section style="height: 400vh">
    <div class="scroll-container">
      <div class="copy-block header" data-start="0" data-end="20">
        <h1>First</h1>
      </div>
      <div class="copy-block footer" data-start="0" data-end="20">
        <h1>First</h1>
      </div>
      <div class="copy-block header" data-start="20" data-end="40">
        <h1>Second</h1>
      </div>
      <div class="copy-block footer" data-start="20" data-end="40">
        <h1>Second</h1>
      </div>
      <div class="copy-block header" data-start="40" data-end="60">
        <h1>Third</h1>
      </div>
      <div class="copy-block footer" data-start="60" data-end="80">
        <h1>Fourth</h1>
      </div>
    </div>
  </section>
</template>

<style lang="scss" scoped>
.read-the-docs {
  color: #888;
}

.progress-bar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 10px;
  background: #646cff;
  transform-origin: left;
}

.scroll-container {
  height: 100vh;
  position: sticky;
  top: 0;
}

.copy-block {
  position: absolute;

  &.header {
    top: 200px;
  }

  &.footer {
    bottom: 200px;
    top: unset;
  }
}
</style>
