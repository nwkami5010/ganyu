<template >
  <Layout class-prefix="layout">


    <NumberPad :value.sync="record.amount"  @submit="saveRecord"/>

    <Tabs :data-source="recordTypeList"/>
    <div class="notes">
    <FormItem :value.sync="record.notes" field-name="备注" placeholder="请在这里输入备注"/>
    </div>
    <Tags :value.sync = "record.tags"/>
  </Layout>



</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

import NumberPad from '@/components/Money/NumberPad.vue';

import Tags from '@/components/Money/Tags.vue';
import FormItem from '@/components/Money/FormItem.vue';
import recordTypeList from '@/constants/recordTypeList';

import Tabs from '@/components/Tabs.vue';






@Component({
  components: {FormItem, Tags,  NumberPad,Tabs},

})
export default class Money extends Vue {

  recordTypeList = recordTypeList;

  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0
  };



  saveRecord(){
    // 深拷贝：先变成字符串，再变成对象，这样就不是同一个内存地址了
    if (!this.record.tags || this.record.tags.length === 0) {
      return window.alert('请选择一个标签');
    }
    this.$store.commit('createRecord', this.record);
    this.record.notes = '';
  }


}
</script>
<style lang="scss">
  .layout-content{

    display:flex;
    flex-direction: column-reverse;
  }
  .notes{
    padding: 12px 0;
  }
</style>
<style lang="scss" scoped>
  @import"~@/assets/style/helper.scss";







</style>
