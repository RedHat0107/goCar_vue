<template>
    <div class="go_buy_subject">
      <div class="go_choose_class">
        <span v-for="(item,index) in goodsClass" :key="index" :class="[classSelect.some(val => val === item.goodsClass) ?'active':'']" @click="handleCLassClick(item.goodsClass)">{{item.goodsText}}</span>
      </div>
      <div class="go_buy_choose">
        <span v-for="(item,index) in goodsYear" v-if="item.isShow" :key="index" :class="[yearSelect.some(val => val === item.goodsYear) ?'active':'']" @click="handleYearClick(item.goodsYear)">{{item.goodsText}}</span>
      </div>
      <div class="go_choose_subject">
          <span
              v-for="(item) in goodsDetails"
              v-bind:key="item.index"
              :class="[select.some(val => val === item.goodsSubject) ?'active':'']"
              @click="handleClick(item.goodsSubject)"
          >{{item.goodsText}}</span>
      </div>
    </div>
</template>

<script>
export default {
    name: "Subject",
    data() {
        return {
            select: [],
            classSelect:[],
            yearSelect:[],
            goodsYear:[
              {
                goodsText:'1年保障',
                goodsYear:'1',
                isShow:true
              },
              {
                goodsText:'2年保障',
                goodsYear:'2',
                isShow:true
              },
              {
                goodsText:'3年保障',
                goodsYear:'3',
                isShow:true
              },
              {
                goodsText:'5年保障',
                goodsYear:'5',
                isShow:false
              }
            ],
            goodsClass:[
              {
                goodsText:'A 超值精品班',
                goodsClass:'A'
              },
              {
                goodsText:'B 名师高效班',
                goodsClass:'B'
              },
            ],
            goodsDetails: [
                {
                    goodsText: "会计",
                    goodsSubject: "kj"
                },
                {
                    goodsText: "审计",
                    goodsSubject: "sj"
                },
                {
                    goodsText: "财务管理",
                    goodsSubject: "cg"
                },
                {
                    goodsText: "经济法",
                    goodsSubject: "jjf"
                },
                {
                    goodsText: "税法",
                    goodsSubject: "sf"
                },
                {
                    goodsText: "战略",
                    goodsSubject: "zl"
                },
                {
                    goodsText: "六科同构",
                    goodsSubject: "tg"
                }
            ]
        };
    },
    methods: {
      handleCLassClick(val){
        if(this.classSelect.some(item=> item ===val)){
          this.classSelect = [];
        }else{
          this.classSelect.push(val);
        }
      },
      handleYearClick(val){
        if(this.yearSelect.some(item=> item ===val)){
          this.yearSelect = [];
        }else{
          this.yearSelect.push(val);
        }
      },
      handleClick(val) {
          if(this.classSelect.length == 0){
            alert('请选择班级！');
            return;
          }else if(this.yearSelect.length == 0){
            alert('请选择年限！');
            return;
          }
          let activeAry = this.select;
          let bol = activeAry.some(item => val === item);
          let ary = [];
          if (val === "tg") {
              ary = bol ? [] : ["tg"];
          } else {
              ary = activeAry.filter(item => item !== "tg");
              if (bol) {
                  ary = ary.filter(item => item !== val);
              } else {
                  ary = [val, ...ary];
              }
          }
          this.select = ary;
      }
    }
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.ljgm {
    font-size: 2rem;
    width: 100%;
    line-height: 4rem;
    text-align: center;
    color: #333;
}
.go_choose_subject {
    margin-top: 1rem;
}
span.active {
    color: #fff;
    background: red !important;
}
.go_choose_subject span {
    display: inline-block;
    padding: 0 1rem;
    line-height: 2rem;
    border-radius: 1rem;
    background: #d8d8d8;
    text-align: center;
    margin-top: 0.5rem;
    margin-right: 0.4rem;
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