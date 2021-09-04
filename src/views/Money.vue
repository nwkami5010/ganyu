<template >
  <Layout class-prefix="layout">


    <NumberPad :value="record.amount" @update:value="onUpdateAmount" @submit="saveRecord"/>
    <!--<Types :value="record.type" @update:value="onUpdateType"/>-->
    <!--传给子组件的value的值是record.type，子组件改的也是record.type，直接value.sync-->
    <Types :value.sync="record.type"/>
    <div class="notes">
    <FormItem field-name="备注" placeholder="请在这里输入备注" @update:value="onUpdateNotes" />
    </div>
    <Tags :value.sync = "record.tags"/>
  </Layout>



</template>

<script lang="ts">
import Vue from 'vue';
import {Component} from 'vue-property-decorator';

import NumberPad from '@/components/Money/NumberPad.vue';
import Types from '@/components/Types.vue';
import Tags from '@/components/Money/Tags.vue';
import FormItem from '@/components/Money/FormItem.vue';







@Component({
  components: {FormItem, Tags,  Types, NumberPad},
  computed: {
    recordList(){
      return this.$store.state.recordList;
    }
  }
})
export default class Money extends Vue {


  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0
  };

  created(){
    this.$store.commit('fetchRecords')
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  onUpdateAmount(value: string) {
    this.record.amount = parseFloat(value);
  }

  saveRecord(){
    // 深拷贝：先变成字符串，再变成对象，这样就不是同一个内存地址了
    this.$store.commit('createRecord', this.record);

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
