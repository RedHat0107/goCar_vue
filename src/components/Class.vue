<template>
  
    
</template>

<script>
export default {
  name: 'Years',
  data:()=>{
    return{
      goodsDetails:[
        {
          goodsText:'A 超值精品班',
          goodsClass:'A'
        },
        {
          goodsText:'B 名师高效班',
          goodsClass:'B'
        },
      ]
    }
  },
  methods:{
    handleClick:(a)=>{
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
  .go_choose_class span{
    display: inline-block;
    padding: 0 1rem;
    line-height: 2rem;
    border-radius: 1rem;
    background: #d8d8d8;
    text-align: center;
    margin-right: .4rem;
  }
</style>
