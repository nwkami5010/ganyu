<template >
  <Layout class-prefix="layout">
    <NumberPad/>
    <Types/>
    <Notes/>
    <Tags data-source="tags"/>

  </Layout>



</template>

<script >


import NumberPad from '@/components/Money/NumberPad.vue';
import Types from '@/components/Types.vue';
import Tags from '@/components/Money/Tags.vue';
import Notes from '@/components/Money/Notes.vue';
export default {
  name: 'Money',
  components: {Notes, Tags, Types, NumberPad},
  data(){
    return {
      tags:['衣','食','住','行']
    }
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
