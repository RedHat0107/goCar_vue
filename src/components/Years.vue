<template>
  <div class="go_buy">
    <div class="go_buy_choose">
      <span v-for="(item,index) in goodsDetails" :index="item.index" @click="goBuy(item.goodsYear)">{{item.goodsText}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Years',
  data:()=>{
    return{
      dataPrice:1234,
      goodsDetails:[
        {
          goodsText:'1科',
          goodsYear:'1'
        },
        {
          goodsText:'2科',
          goodsYear:'2'
        },
      ]
    }
  },
  methods:{
    goBuy:(a)=>{
      console.log(a);
    }
  }
}
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .ljgm{
    font-size: 2rem;
    width: 100%;
    line-height: 4rem;
    text-align: center;
    color: #333;
  }
  .go_buy_choose{
      margin-top: 1rem;
  }
  .go_buy_choose span{
    display: inline-block;
    width: 5rem;
    line-height: 2rem;
    border-radius: 1rem;
    background: #d8d8d8;
    text-align: center;
    margin-top: .5rem;
    margin-right: .4rem;
  }
</style>
