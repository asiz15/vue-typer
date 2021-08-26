<template>
  <span>
    {{ titleRender }}
    <span class="cursor" :class="{ typing: typeStatus }">&nbsp;</span>
  </span>
</template>
<script>
export default {
  props: {
    title: {
      type: String,
    },
  },
  data() {
    return {
      titleRender: "",
      titleIterator: 0,
    };
  },
  methods: {
    typing() {
      if (this.titleIterator < this.title.length) {
        this.titleRender += this.title.charAt(this.titleIterator);
        this.titleIterator++;
        setTimeout(this.typing, 50);
      } else {
        this.titleIterator = 0;
        setTimeout(this.erase, 1000);
      }
    },
    erase() {
      if (this.titleRender.length > 0) {
        this.titleRender = this.titleRender.split("");
        this.titleRender.splice(this.titleRender.length - 1, 1);
        this.titleRender = this.titleRender.join("");

        setTimeout(this.erase, 30);
      }
    },
  },
};
</script>
<style lang="scss" scoped>
@keyframes cursorBlink {
  49% {
    background-color: #fff;
  }
  50% {
    background-color: transparent;
  }
  99% {
    background-color: transparent;
  }
}

span.cursor {
  display: inline-block;
  margin-left: 3px;
  width: 4px;
  line-height: 0.9em;
  background-color: #000;
  animation: cursorBlink 1s infinite;
}
</style>