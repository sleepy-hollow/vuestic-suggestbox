<template>
  <div class="dashboard">
    <vuestic-widget headerText="SuggestBox">
      value: {{ value }}
      <div class="www">
        <suggest-box :suggestions="suggestList" v-model="value"></suggest-box>
      </div>
    </vuestic-widget>
  </div>
</template>

<script>
  import SuggestBox from '../SuggestBox.vue'

  export default {
    name: 'dashboard',
    components: {
      SuggestBox
    },
    data () {
      return {
        value: '',
        suggestList: [
          { name: '夏休み' },
          { name: 'アッコ' },
          { name: 'ロッテ' },
          { name: 'スーシー' },
          { name: 'ダイアナ' },
          { name: 'リンゴ' },
          { name: 'もも' },
          { name: '春' },
          { name: '池' },
          { name: '雪' },
          { name: '夏休み' }
        ]
      }
    }
  }
</script>

<style lang="scss" scoped>
  @import "../../sass/_variables.scss";
  .www {
    width: 300px;
  }
</style>
