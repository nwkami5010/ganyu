<template>
  <div>
    <label class="notes">
      <span class="name">  备注</span>
      <!--当input的value等于输入的value，可以用v-model代替-->
      <input type="text" v-model="value"

             placeholder="在这里输入备注">
    </label>

  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

@Component
export default class Notes extends Vue {
  value = '';

}
</script>

<style lang="scss" scoped>
.notes{
  font-size: 14px;
  background: #f5f5f5;
  // display: block;//label默认display:inlineblock,改成block才能显示上面背景
  padding-left:  16px;
  display: flex;//拉长宽度
  align-items: center;
  .name{
    padding-right: 16px;
  }
  input{
    height:64px;//height line-height都可以 64px
    flex-grow: 1;//尽量不写宽度
    background: transparent;
    border: none;
    padding-right: 16px;
  }
}
</style>
