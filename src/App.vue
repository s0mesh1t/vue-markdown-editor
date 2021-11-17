<template>
    <MarkdownEditor></MarkdownEditor>
</template>

<script>
import MarkdownEditor from "@/components/MakrdownEditor"

export default {
  components: {MarkdownEditor}
}

</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700,900&display=swap");

body {
  font-family: "Montserrat", sans-serif;
  background-color: #1B2B34;
  padding: 0;
  max-width: none;
}
</style>
