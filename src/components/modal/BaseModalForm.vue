<template>
    <div class="dialog-Customer" v-show="active">  
      <slot></slot>
    </div>
</template>

<script>
export default {

  data(){
    return{
      active:false,
    }
  },

  methods:{
    show(){
      this.active = true
    },

    hide(){
      this.active = false
    }
  }
}
</script>

<style scoped>

</style>