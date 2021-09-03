<template >
  <Layout class-prefix="layout">


    <NumberPad :value="record.amount" @update:value="onUpdateAmount" @submit="saveRecord"/>
    <!--<Types :value="record.type" @update:value="onUpdateType"/>-->
    <!--传给子组件的value的值是record.type，子组件改的也是record.type，直接value.sync-->
    <Types :value.sync="record.type"/>
    <Notes @update:value="onUpdateNotes"/>
    <Tags :data-source.sync="tags" @update:value="onUpdateTags"/>
  </Layout>



</template>

<script lang="ts">
import Vue from 'vue';
import {Component,Watch} from 'vue-property-decorator';

import NumberPad from '@/components/Money/NumberPad.vue';
import Types from '@/components/Types.vue';
import Tags from '@/components/Money/Tags.vue';
import Notes from '@/components/Money/Notes.vue';
import {recordListModel} from '@/models/recordListModel';
import {tagListModel} from '@/models/tagListModel';



const recordList = recordListModel.fetch();
const tagList = tagListModel.fetch();
type Record = {
  tags: string[];
  notes: string;
  type: string;
  amount: number;
  createdAt?: Date;
}

@Component({
  components: {Tags, Notes, Types, NumberPad}
})
export default class Money extends Vue {
  tags = tagList;
  recordList: RecordItem[] = recordList;
  record: RecordItem = {
    tags: [], notes: '', type: '-', amount: 0
  };

  onUpdateTags(value: string[]) {
    this.record.tags = value;
  }

  onUpdateNotes(value: string) {
    this.record.notes = value;
  }

  onUpdateAmount(value: string) {
    this.record.amount = parseFloat(value);
  }

  saveRecord(){
    // 深拷贝：先变成字符串，再变成对象，这样就不是同一个内存地址了
    const record2 :RecordItem = recordListModel.clone(this.record);
    record2.createdAt = new Date();
    this.recordList.push(record2);
    console.log(this.recordList);
  }

  @Watch('recordList')
  onRecordListChange() {
    recordListModel.save(this.recordList);
  }

}
</script>
<style lang="scss">
  .layout-content{

    display:flex;
    flex-direction: column-reverse;
  }
</style>
<style lang="scss" scoped>
  @import"~@/assets/style/helper.scss";







</style>
