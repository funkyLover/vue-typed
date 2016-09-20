<template>
  <span>{{ typed }}</span>
</template>

<script>
export default {
  props: {
    entireness: {
      type: String,
      required: true
    },
    during: {
      // ms
      type: Number,
      default: 200
    },
    delay: {
      type: Number,
      default: 1000
    },
    completeFn: Function
  },
  data () {
    return {
      typed: '',
      timeSlice: 16,
      strIndex: 0
    }
  },
  mounted () {
    var _ = this
    var length = _.entireness.length
    _.timeSlice = _.during / length
    setTimeout(function () {
      _.type()
    }, _.delay)   
  },
  methods: {
    type () {
      var _ = this
      if (_.strIndex < _.entireness.length) {
        _.completeFn && _.completeFn()
        return
      } else {
        setTimeout(function () {
          _.typed += _.entireness[_.strIndex] 
          _.strIndex += 1
          _.type()
        }, _.timeSlice)
      }
    }
  }
}
</script>
