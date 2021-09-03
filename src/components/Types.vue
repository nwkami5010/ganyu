<template>
  <div><ul class="types">
    <li :class="type === '-' && selected"
    @click="selectType('-')">支出</li>
    <li :class="type === '+' && selected"
    @click="selectType('+')">收入</li>
  </ul></div>
</template>

<script lang="ts">
import Vue from 'vue'
import {Component, Prop} from 'vue-property-decorator';
@Component
export default class Types extends Vue{
   @Prop() readonly  value!: string;//'-'表示支出，‘+表示’收入

    selectType(type: string){//type只能是‘-’和‘+’
      if(type!=='-' && type!=='+'){
        throw new Error('type is unknown')
      }
      this.$emit('update:value',type) ;
    }
  }

</script>

<style lang="scss" scoped>
.types{
  background: #c4c4c4;
  display: flex;
  text-align: center;//字居中
  font-size: 24px;
  >li{
    width: 50%;//不用具体宽度
    //line-height:  64px;
    height: 64px;//如果有border会超过64px
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    &.selected::after{//当前li被选中
      //border-bottom:  4px solid;选中会影响字体居中
      content: '';
      position: absolute;
      bottom:0;
      left: 0;//不写left有问题
      width: 100%;
      height: 4px;
      background: #333;
    }
  }
}
</style>