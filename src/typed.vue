<template>
  <span class="typed">{{ typed }}<span class="cursor" v-if="shouldShowCursor">{{ cursorChar }}</span></span>
</template>
<script>
export default {
  props: {
    str: {
      type: String,
      required: true
    },
    typeSpeed: {
      // ms
      type: Number,
      default: 20
    },
    delay: {
      type: Number,
      default: 1000
    },
    cursorChar: {
      type: String,
      default: '|'
    },
    cleanCursor: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      typed: '',
      strIndex: 0,
      sentenceIndex: 0,
      shouldShowCursor: true
    }
  },
  mounted () {
    var _ = this
    // make typeSpeed not less than 16
    _.typeSpeed = Math.max(_.typeSpeed, 16)
    // delay start to type
    setTimeout(function () {
      _.type()
    }, _.delay)   
  },
  methods: {
    type () {
      var _ = this
      if (_.strIndex === _.str.length) {
        // type finish!
        if (_.cleanCursor) {
          _.shouldShowCursor = false
        }
        _.$emit('done')
        return
      } else {
        setTimeout(function () {
          _.typed += _.str[_.strIndex] 
          _.strIndex += 1
          _.type()
        }, _.typeSpeed)
      }
    }
  }
}
</script>

<style scoped>

.typed {
  white-space: pre;
}

.cursor {
  opacity: 1;
  font-weight: 100;
  animation: blink 0.7s infinite;
}

@keyframes blink {
  0% {
    opacity: 1; 
  }
  50% {
    opacity: 0; 
  }
  100% {
    opacity: 1; 
  } 
}

</style>
