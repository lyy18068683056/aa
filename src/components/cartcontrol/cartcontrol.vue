<template>
  <div class="cartcontrol">
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
    <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0"></div>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle"></div>
=======
    <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart"
     transition="move">
      <span class="inner  icon-remove_circle_outline"></span>
    </div>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click="addCart"></div>
>>>>>>> 购物车组件的实现
  </div>
</template>

<script>
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
=======
	import Vue from 'vue';
>>>>>>> 购物车组件的实现
  export default{
    props:{
      food:{
        type:Object
      }
    },
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
    created(){
        console.log(this.food)
    }
=======
   methods:{
   	addCart(event){
   		//在PC端晕倒点击触发两次的问题,在参数里添加event 写一个判断
   		if(!event._constructed){
   			return;
   		}
   		if(!this.food.count){
   			//通过vue.set去添加一个属性的时候
   			Vue.set(this.food,'count',1)
   		}else{
   			this.food.count++;
   		}
      this.$dispatch('cart.add',event.target);
   	},
   	decreaseCart(event){
   		if(!event._constructed){
   			return;
   		}
   		if(this.food.count){
   			this.food.count--;
   		}
   	}
   }
>>>>>>> 购物车组件的实现
  }
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size :0
    .cart-decrease
      display:inline-block
      padding :6px
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
      font-size :24px
      line-height :24px
    .cart-count
      display :inline-block
    .cart-add
      display :inline-block
      font-size :24px
      line-height :24px
=======
      transition:all 0.4s linear
      &.move-transition
        opacity:1
        transform:translate3d(0,0,0)
        .inner
          font-size :24px
          line-height :24px
          color:rgb(0,160,220)
          display:inline-block
          transition:all 0.4s linear
          transform:rotate(0)
      &.move-enter,&.move-leave
        opacity:0
        transform:translate3d(24px,0,0)
        .inner
          transform:rotate(180deg)
    .cart-count
      display :inline-block
      vertical-align:top
      width:12px
      padding-top:6px
      line-height:24px
      text-align:center
      font-size:10px
      color:rgb(147,153,159)
    .cart-add
      display :inline-block
      padding :6px
      font-size :24px
      line-height :24px
      color:rgb(0,160,220)
>>>>>>> 购物车组件的实现
</style>
