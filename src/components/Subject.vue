<template>
    <div class="go_buy_subject">
        <div class="go_choose_class">
            <span>价格:{{price}}</span>
        </div>
        <div class="go_choose_class">
            <span
                v-for="(item,index) in goodsClass"
                :key="index"
                :class="[classSelect ===item.goodsClass ?'active':'']"
                @click="handleCLassClick(item.goodsClass)"
            >{{item.goodsText}}</span>
        </div>
        <div class="go_buy_choose">
            <span
                v-for="(item,index) in goodsYear"
                :key="index"
                :class="[yearSelect === item.goodsYear ?'active':'']"
                @click="handleYearClick(item.goodsYear)"
            >{{item.goodsText}}</span>
        </div>
        <div class="go_choose_subject">
            <span
                v-for="(item) in goodsDetails"
                v-bind:key="item.index"
                :class="[select.some(val => val === item.goodsSubject) ?'active':'']"
                @click="handleClick(item.goodsSubject)"
            >{{item.goodsText}}</span>
        </div>
        <button @click="handleBuy">购买</button>
    </div>
</template>

<script>
const defaultYear = [
    {
        goodsText: "1年保障",
        goodsYear: "1"
    },
    {
        goodsText: "2年保障",
        goodsYear: "2"
    },
    {
        goodsText: "3年保障",
        goodsYear: "3"
    },
    {
        goodsText: "5年保障",
        goodsYear: "5"
    }
];
const defaultSubject = [
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
];
export default {
    name: "Subject",
    data() {
        return {
            allPrice:lessonJson.price,
            allId:lessonJson.lessonId,
            select: [],
            classSelect: "",
            yearSelect: "",
            goodsYear: defaultYear,
            price: 0,
            goodsClass: [
                { goodsClass: "A", goodsText: "A 超值精品班" },
                { goodsClass: "B", goodsText: "B 名师高效班" },
                { goodsClass: "C", goodsText: "C 智能题库班" },
                { goodsClass: "D", goodsText: "A+B+C 畅听无忧班" },
            ],
            goodsDetails: defaultSubject
        };
    },
    watch: {
        classSelect: function() {
            let bol = this.classSelect == 'D';
            if (bol) {
                this.price = this.allPrice[this.classSelect + 36];
                this.yearSelect = '3';
                this.select = ['tg'];
            } else {
                this.price = this.allPrice[this.classSelect + 11];
                this.yearSelect = '1';
                this.select = [];
            }
            
            console.log(this.price);
        },
        yearSelect: function() {
            let bol = this.yearSelect == 3 || this.yearSelect == 5;
            
            if (bol) {
                this.price = this.allPrice[this.classSelect + this.yearSelect + 6];
                this.select = ['tg'];
            } else {
                this.price = this.allPrice[this.classSelect + this.yearSelect + 1];
                this.select = [];
            }
        },
        select: function() {
            const len = this.select.length || 1;
            let bol = this.select.some(item => "tg" === item);
            if (bol) {
                this.price = this.allPrice[this.classSelect + this.yearSelect + 6];
            } else {
                this.price = this.allPrice[this.classSelect + this.yearSelect + len];
            }
        }
    },
    methods: {
        handleCLassClick(val) {
            this.classSelect = val;
            if (val === "D") {
                this.goodsYear = [
                    {
                        goodsText: "3年",
                        goodsYear: "3"
                    },
                    {
                        goodsText: "5年",
                        goodsYear: "5"
                    }
                ];
                this.goodsDetails = [
                    {
                        goodsText: "六科同构",
                        goodsSubject: "tg"
                    }
                ];
            }else{
                this.goodsYear = defaultYear;
                this.goodsDetails = defaultSubject;
            }
        },
        handleYearClick(val) {
            this.yearSelect = val;
            if(val == 3 || val == 5){
                this.goodsYear = [
                    {
                        goodsText: "3年",
                        goodsYear: "3"
                    },
                    {
                        goodsText: "5年",
                        goodsYear: "5"
                    }
                ];
                this.goodsDetails = [
                    {
                        goodsText: "六科同构",
                        goodsSubject: "tg"
                    }
                ];
            }else{
                this.goodsYear = defaultYear;
                this.goodsDetails = defaultSubject;
            }
        },
        handleClick(val) {
            if (this.classSelect.length == 0) {
                alert("请选择班级！");
                return;
            } else if (this.yearSelect.length == 0) {
                alert("请选择年限！");
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
        },
        handleBuy() {
            const selectSubjet = this.select;
            let gc = new Object();
            gc.goodsList = new Array();
            for(let i = 0; i < selectSubjet.length; i++){
                let cur = selectSubjet[i];
                let curId = this.allId[this.classSelect + this.yearSelect + cur];
                for(let j = 0; j < curId.dataId.split(" ").length; j++){
                    let goods = new Object();
                    goods.pid = curId.dataId.split(" ")[j];
                    goods.pclassific = 2;
                    goods.venderId = 1;
                    goods.promoId = curId.proId;
                    gc.goodsList.push(goods);
                }
            }
            let goodsInfo = JSON.stringify(gc);
            console.log(goodsInfo);
            if (gc.goodsList.length != 0) {
                window.location.href = "http://p.m.dongao.com/shopping/addCart.html?buyGoodsInfo=" + goodsInfo;
            }
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
.go_choose_class span {
    display: inline-block;
    padding: 0 1rem;
    line-height: 2rem;
    border-radius: 1rem;
    background: #d8d8d8;
    text-align: center;
    margin-right: 0.4rem;
}
.go_buy_choose span {
    display: inline-block;
    width: 5rem;
    line-height: 2rem;
    border-radius: 1rem;
    background: #d8d8d8;
    text-align: center;
    margin-top: 0.5rem;
    margin-right: 0.4rem;
}
</style>