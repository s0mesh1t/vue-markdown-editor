<template>
  <div class="markdown-editor">
    <div class="pre">
      <textarea v-model="preMark" ></textarea>
    </div>
    <div class="post" >
      <div v-html="postMark"></div>
    </div>
  </div>
</template>

<script>
import { marked } from 'marked'
import {ref, computed, onMounted, watch} from "vue"

export default {
  setup() {
    const preMark = ref("# Hello World\n ### List\n - item 1\n - item 2\n - item 3\n\n [Google](google.com)")

    const postMark = computed({
      get: () => marked(preMark.value, {breaks: true, smartypants: true}),
    })

    onMounted(() => {
      if (localStorage.preMark) {
        preMark.value = localStorage.preMark;
      }
    })

    watch(preMark, (val, newVal) => {
      localStorage.preMark = newVal
      console.log(preMark.value)
    })

    return { preMark, postMark }
  }
}
</script>

<style lang="scss" scoped>
.markdown-editor {
  margin: 10vh 10vw;
  padding: 20px;
  min-height: 79vh;
  border-radius: 6px;
  background-color: #eeeeee;
  border: solid 2px #efefef;
  opacity: 0.9;
  white-space: nowrap;
  color: #1B2B34;
  box-shadow: 1px 1px 14px #8FBCBB;

  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  @media screen and (max-width: 868px) {
    grid-template-columns: repeat(1, 1fr);
  }
}

.pre textarea {
  width: 100%;
  height: 100%;
  padding: 10px;
  resize: none;
  background: none;
  border: none;
  box-sizing: border-box;
  font-size: 15px;
  color: #1B2B34;
  outline: 2px solid #ccc;
}

.post {
  color: #1B2B34;
  font-size: 17px;
}
.post div {
  padding-left: 10px;
  height: 100%;
  width: 100%;
  overflow-y: scroll;
}
</style>