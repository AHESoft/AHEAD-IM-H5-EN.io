<template>
  <div class="g-inherit m-main p-general" v-if="myInfo.account">
    <group class="u-card">
      <cell :title="myInfo.nick" :inline-desc="'Account: ' + myInfo.account">
        <img class="icon" slot="icon" width="20" :src="myInfo.avatar">
      </cell>
    </group>
    <group class="u-card">
      <cell title="Nickname">{{myInfo.nick || ''}}</cell>
      <cell title="Gender">{{myInfo.gender}}</cell>
      <cell title="Birthday">{{myInfo.birth}}</cell>
      <cell title="Mobile">{{myInfo.tel}}</cell>
      <cell title="Mail">{{myInfo.email}}</cell>
      <cell title="Saying">{{myInfo.sign}}</cell>
    </group>
    <div>
      <x-button type="warn" action-type="button" @click.native="logout">注销</x-button>
    </div>
  </div>
</template>

<script>
import { Group, Cell } from 'vux'

export default {
  components: {
    Group,
    Cell
  },
  computed: {
    myInfo () {
      return this.$store.state.myInfo
    }
  },
  methods: {
    logout () {
      let that = this
      this.$vux.confirm.show({
        title: 'Sure要注销Account？',
        onConfirm () {
          that.$store.dispatch('logout')
        }
      })
    }
  }
}
</script>
