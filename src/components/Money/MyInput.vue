<template>
  <div>
    <input :value="value" @input="onInput"/> //用户在input上修改时，必须在input上绑定你得到的外部value，
    //input变化时不能直接改value值
  </div>
</template>

<script lang="js">

export default {
    name: 'MyInput',
    props:{//接受一个值叫value,类型string
      value:{
        type:String
      }
    },
    methods: {//添加事件
      onInput(e){//当input触发了oninput后，就再次emit一个input事件，需要包装一个有target.value的event
        const value =  e.target.value;
        this.$emit('input',value)
      }
    }
}
</script>

<style lang="scss" scoped>

</style>