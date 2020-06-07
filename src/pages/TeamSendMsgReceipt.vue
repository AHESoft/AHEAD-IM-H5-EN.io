<template>
  <div class='g-inherit m-article p-msg-receipt'>
    <x-header class="m-tab" :left-options="{backText: ' '}">
      <h1 class="m-tab-top">发送已读Receipt消息</h1>
      <a slot="left"></a>
    </x-header>
    <div class="g-body">
      <group>
        <x-textarea v-model='inputMsg' placeholder="输入消息内容"></x-textarea>
        <x-button type='primary'  @click.native='sendMsg'>发送</x-button>
      </group>
      <p class='tip'>
         图片、音频、视频、文件、自定义等消息类型。此处仅以文本消息作为演示，开发者可以根据具体业务场景进行功能设计。
      </p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      inputMsg: ''
    }
  },
  computed: {
    to() {
      return this.$route.params.teamId
    }
  },
  methods: {
    sendMsg() {
      if (/^\s*$/.test(this.inputMsg)) {
        this.$vux.alert.show({
          title: 'Please do not send an empty message.'
        })
        return
      }
      this.$store.dispatch('sendMsg', {
        type: 'text',
        scene: 'team',
        to: this.to,
        text: this.inputMsg,
        needMsgReceipt: true
      })
      history.go(-1)
    }
  }
}
</script>

<style>
  .p-msg-receipt {
    background-color: #ebeef3;

    .tip {
      padding: 1rem;
      color: #666;
    }
  }
</style>
