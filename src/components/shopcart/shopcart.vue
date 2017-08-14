<template>
  <div class="shopcart">
    <div class="content">
      <!--左侧-->
      <div class="content-left">
        <div class="logo-wrapper">
          <!--logo-->
          <div class="logo" :class="{'highlight':totalCount>0}">
            <i class="icon-shopping_cart"  :class="{'highlight':totalCount>0}"></i>
          </div>
          <!--选择商品的数量-->
          <div class="num" v-show="totalCount>0">{{totalCount}}</div>
        </div>
        <!--配送费-->
        <div class="price"  :class="{'highlight':totalPrice>0}">￥{{totalPrice}}</div>
        <!--配送价-->
        <div class="desc">另需配送费￥{{deliveryPrice}}元</div>
      </div>
      <!--右侧-->
      <div class="content-right">
        <div class="pay" :class="payClass">
          {{payDesc}}
        </div>
      </div>
    </div>
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
=======
    <!--添加商品到购物车产生一个动画小球-->
    <div class="ball-container">
      <div transition="drop" v-for="ball in balls" v-show="ball.show" class="ball">
        <div class="inner inner-hook"></div>
      </div>
    </div>
>>>>>>> 购物车组件的实现
  </div>
</template>

<script type="text/ecmascript-6">
  export default{
    props: {
        selectFoods:{   //        选择的食物作为一个数组
          type:Array,
          default(){
            return [
//                用来存放数组里每一个物品的价格和数量
              {
                  price:60,
                count:1
              }
            ];
          }
        },
      deliveryPrice: {   //      另需配送费
        type: Number,
        default: 0
      },
      minPrice: {  //      多少钱起送
        type: Number,
        default: 0
      }
    },
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
=======
    data(){
      return{
        balls:[
          {
            show:false
          },
          {
            show:false
          },
          {
            show:false
          },
          {
            show:false
          },
          {
            show:false
          }
        ],
        dropBalls:[]
      }
    },
>>>>>>> 购物车组件的实现
    computed:{
        totalPrice(){   //        计算总价
            let total=0;
           this.selectFoods.forEach((food) => {
              total += food.price * food.count
           });
           return total;
        },
        totalCount(){   //计算总数量
            let count=0;
            this.selectFoods.forEach((food) => {
                count += food.count;
            })
          return count;
        },
      payDesc(){   //      右边的还差多少起送
        if(this.totalPrice === 0){
           return `￥${this.minPrice}元起送`;
        }else if(this.totalPrice < this.minPrice){
            let diff=this.minPrice - this.totalPrice;
            return `还差￥${diff}元起送`;
        }else{
            return '去结算';
        }
      },
      payClass(){   //计算价格来添加相应的样式
          if(this.totalPrice < this.minPrice){
              return 'no-enough';
          }else{
              return 'enough';
          }
      }
<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
    }
  }
=======
    },
    methods:{
//      添加商品抛物线的动画效果
      drop(el){
        for(let i=0;i<this.balls.length;i++){
          let ball=this.balls[i];
          if(!this.ball){
            ball.show=true;
            ball.el=el;
            this.dropBalls.push(ball);
            return;
          }
        }
      }
    },
//    transition的动画效果
    transitions:{
      drop:{
        beforeEnter(el) {
          let count =this.balls.length;
          while(count--){
            let ball=this.balls[count];
            if(ball.show){
              let rect=ball.el.getBoundingClientRect();
              let x=rect.left-32;
              let y=-(window.innerHeight - rect.top - 22);
              el.style.display=' ';
              el.style.webkitTransform=`translate3d(0,${y}px,0)`;
              el.style.transform=`translate3d(0,${y}px,0)`;
              let inner=el.getElementsByClassName('inner-hook')[0];
              inner.style.webkitTransform=`translate3d(${x}px,0,0)`;
              inner.style.transform=`translate3d(${x}px,0,0)`;
            }
          }
        },
        enter(el) {
          let rf=el.offsetHeight;
          this.$nextTick(() => {
            el.style.webkitTransform='translate3d(0,0,0)';
            el.style.transform='translate3d(0,0,0)';
            let inner=el.getElementsByClassName('inner-hook')[0];
            inner.style.webkitTransform='translate3d(0,0,0)';
            inner.style.transform='translate3d(0,0,0)';
          });
        },
        afterEnter(el) {
          let ball=this.dropBalls.shift();
          if(ball){
            ball.show=false;
            el.style.display='none';
          }
        }
      }
    }
  };
>>>>>>> 购物车组件的实现
</script>

<style lang="stylus" type="text/stylus" rel="stylesheet/stylus">
  .shopcart
    position:fixed
    left:0
    bottom:0
    z-index :50
    width:100%
    height:48px
    /*底部*/
    .content
      display:flex
      background :#1d1427
      font-size :0
      color:rgba(255,255,255,0.4)
      /*底部左*/
      .content-left
        flex :1
        .logo-wrapper
          display :inline-block
          position :relative
          top: -10px
          margin:0 12px
          padding:6px
          width:56px
          height:56px
          box-sizing :border-box
          vertical-align :top
          border-radius :50%
          background :#1d1427
          /*底部左logo*/
          .logo
            width:100%
            height:100%
            border-radius :50%
            background :#2b343c
            text-align :center
            /*购物车有数量的时候logo亮*/
            &.highlight
              background :rgb(0,160,220)
            .icon-shopping_cart
              font-size :24px
              line-height :44px
              color:#80858a
              &.highlight
                color:rgb(255,255,255)
              /*商品的数量*/
          .num
            position :absolute
            top:0
            right:0
            width: 24px
            height:16px
            line-height :16px
            font-weight :700
            text-align :center
            border-radius :16px
            font-size :9px
            background:rgb(240,20,20)
            box-shadow:0 4px 8px 0 rgba(0,0,0,0.4)
        .price
          display :inline-block
          font-size :16px
          line-height :24px
          font-weight :700
          vertical-align :top
          margin-top:12px
          box-sizing :border-box
          padding-right:12px
          border-right:1px solid rgb(255,255,255,0.1)
          color:rgba(255,255,255,0.4)
          &.highlight
            color:#fff
        .desc
          display :inline-block
          vertical-align :top
          font-size :10px
          line-height :24px
          font-weight :700
          margin:12px 0 0 12px
      .content-right
        flex:0 0 105px
        width:105px
        .pay
          height: 48px
          line-height :48px
          text-align :center
          font-size :12px
          font-weight :700
          background :#2b333b
          /*去结算的样式*/
          &.not-enough
            background :#2b333b
          &.enough
            background :#00b43c
            color:#fff

<<<<<<< a45c7188fd48a83b0b3a897f284da9f308fe2214
=======
    .ball-container
      .ball
        position:fixed
        left:32px
        bottom:22px
        z-index:200
        &.drop-transition
          transition:all 0.4s cubic-bezier(0.49,-0.29,0.75,0.41)
          .inner
            width:16px
            height:16px
            border-radius:50%
            background:rgb(0,160,220)
            transition:all 0.4s linear
>>>>>>> 购物车组件的实现
</style>
