<template>
  <div class="tags">
    <div class="new">
      <button @click="create">新增标签</button>
    </div>
    <ul class="current">
      <li v-for="tag in dataSource" :key="tag"
          :class="{selected: selectedTags.indexOf(tag)>=0} "
          @click="toggle(tag)">{{tag}}</li>
    </ul>

  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import {Component, Prop} from 'vue-property-decorator';
@Component
export default class Tags extends Vue{
  // readonly外部数据只读
  @Prop() readonly dataSource: string[] | undefined;
  selectedTags: string[] = [];
  toggle(tag: string){
    const index = this.selectedTags.indexOf(tag)
    if(index>=0){
      this.selectedTags.splice(index,1)
    }
    this.selectedTags.push(tag)
  }
  create(){
    const name = window.prompt('请输入标签名');
    if (name === '') {
      window.alert('标签名不能为空');
    } else if (this.dataSource) {//把更新datasource的请求告诉外部，外部接受这个事件，触发了updatedatasorce，就会把数组赋值给datasource
      this.$emit('update:dataSource',[...this.dataSource,name])
    }
  }
}
</script>

<style lang="scss" scoped>
.tags {
  font-size: 14px;
  padding: 16px;
  flex-grow:1;
  display: flex;
  flex-direction: column-reverse;
  > .current {
    display: flex;
    flex-wrap:wrap;

    > li {
      $bg: #d9d9d9;
      background: $bg;
      $h: 24px;
      height: $h;
      line-height: $h;
      border-radius: $h/2;
      padding: 0 16px;
      margin-right: 12px;
      margin-top: 4px;
      &.selected{
        background: #2b2e4a;
        color:white;
      }
    }
  }

  > .new {
    padding-top: 16px;

    button {
      background: #2b2e4a;
      border: none;
      color: #999;
      border-bottom: 1px solid;
      padding: 0 4px;

    }
  }
}
</style>
