<template>
  <div id="web-socket"></div>
</template>

<script>
export default {
  name: "WebSocket",
  props: {
    liveId: {
      type: String
    },
    userId: {
      type: String
    },
    message: {
      type: String
    }
  },
  data() {
    return {
      websocket: null
    }
  },
  created() {
    this.initWebSocket()
  },
  destroyed() {
    this.websocket.close()
  },
  methods: {
    initWebSocket() {
      const wsUrl = "ws://47.108.151.199:8088/message/" + this.liveId + "/" + this.userId
      this.websocket = new WebSocket(wsUrl)
      this.websocket.onopen = this.onOpen
      this.websocket.onmessage = this.onMessage
      this.websocket.onerror = this.onError
      this.websocket.onClose = this.onClose
    },
    onOpen() {
      console.log("弹幕获取成功")
    },
    onMessage(message) {
      this.$emit("onMessage", JSON.parse(message.data));
    },
    onError() {
      console.log("弹幕连接失败，重连...")
      this.initWebSocket()
    },
    onClose() {
      console.log("断开弹幕连接")
    },
    sendMessage(message) {
      this.websocket.send(message)
    }
  },
}
</script>

<style scoped>

</style>
