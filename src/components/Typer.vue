<template>
  <span :style="textStyles">
    {{ titleRender }}
    <span class="cursor" :class="[typingStatus ? 'typing' : '']" :style="{width: cursorWidth, background: typingStatus ? cursorActiveColor : (cursorDefaultColor) ? cursorDefaultColor : 'grey' }">&nbsp;</span>
  </span>
</template>
<script>
export default {
  props: {
    phrases: {
      type: Array,
    },
    textStyles:{
      type: Object,
      default: () => {
        return {}
      }
    },
    cursorWidth:{
      type: String,
      default: '3px'
    },
    cursorActiveColor:{
      type: String,
      default: '#41B883'
    },
    cursorDefaultColor:{
      type: String
    }
  },
  data() {
    return {
      titleRender: "",
      phraseIterator: 0,
      typingStatus: false,
    };
  },
  mounted() {
    setTimeout(this.typing, 2000);
  },
  computed: {
    
  },
  methods: {
    animatePhrase() {
      let phrase = this.phrases[this.phraseIterator];
      if (this.titleRender.length < phrase.length) {
        this.typingStatus = true;
        this.titleRender += phrase.charAt(this.titleRender.length);
        setTimeout(this.animatePhrase, 70);
      } else {
        this.typingStatus = false;
        setTimeout(this.erase, 1200);
      }
    },
    typing() {
      if (this.phraseIterator < this.phrases.length) {
        this.animatePhrase(this.phraseIterator);
      } else {
        this.reset();
      }
    },
    reset() {
      this.phraseIterator = 0;
      setTimeout(() => {
        this.typing();
      }, 2000);
    },
    erase() {
      if (this.titleRender.length > 0) {
        this.typingStatus = true;
        this.titleRender = this.titleRender.split("");
        this.titleRender.splice(this.titleRender.length - 1, 1);
        this.titleRender = this.titleRender.join("");
        setTimeout(this.erase, 40);
      } else {
        this.typingStatus = false;
        setTimeout(() => {
          this.phraseIterator++;
          this.typing();
        }, 500);
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
  width: 3px;
  line-height: 0.9em;
  animation: cursorBlink 0.8s infinite;
}
.typing {
  animation: none !important;
}
</style>
