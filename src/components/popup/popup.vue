<template>
  <div :class="['custom-popup',value&&'active',type]">
    <div class="custom-popup-mask"  @click="hide"></div>
    <div class="custom-popup-content">
      <slot></slot>
    </div>
  </div>
</template>
<script>
  export default {
    name:'popup',
    props:["value","type"],
    methods:{
      hide(){
        this.$emit("input",false);
        this.$emit("change",false);
      },
      show(){
        this.$emit("input",true);
        this.$emit("change",true);
      },
      toggle(){
        let b = !this.value;
        this.$emit("input",b);
        this.$emit("change",b);
      }
    }
  }
</script>
<style lang="scss">
  .custom-popup {
    /*这个方法失效*/
    /*box-shadow: 0 0 1000rpx rgba(0,0,0,0.5);*/
    z-index: 11;

    &.right{
      .custom-popup-content{
        right: 0;
        top: 0;
        bottom: 0;
        left: unset;
        transform: translate3d(100%,0,0);
      }
    }

    &.active{
      .custom-popup-content{
        transform: translate3d(0,0,0);
      }

      .custom-popup-mask{
        display: block;
      }
    }

    .custom-popup-mask{
      position: fixed;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      z-index: 10;
      background: rgba(0, 0, 0, 0.7);
      display: none;
    }

    .custom-popup-content{
      padding: 0 20rpx;
      background-color: #fff;
      transform: translate3d(0,100%,0);
      transition:transform 0.3s ease;
      position: fixed;
      z-index: 12;
      bottom: 0;
      left: 0;
      right: 0;


    }


  }
</style>
