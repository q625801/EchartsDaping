<template>
    <div class="wrap-app">
        <div class="wrap">
            <header class="e-header clear">
                <div class="header-btn clear">
                    <div class="logo fl" ></div>
                    <div class="fl btn-list btn-mrg on">XXXXX</div>
                    <!-- <div class="fl btn-list">能源数据监测</div> -->
                    <!-- <div class="fl btn-bg clear">
                        <div class="carbon fl">
                            <span class="num">355</span>
                            <span class="text">XXXX</span>
                        </div>
                        <div class="carbon carbon-tree fl">
                            <span class="num">123</span>
                            <span class="text">XXXX</span>
                        </div>
                    </div>-->
                </div>
            </header>
            <div class="wrap-echarts">
                <echarts-map></echarts-map>
                <div class="right-info">
                    <censusinfo></censusinfo>
                </div>
                <div class="line-bar clear">
                    <chargdataanalysis></chargdataanalysis>
                    <chargtransactionstatistics></chargtransactionstatistics>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import EchartsMap from './EchartsMap';
import Chargdataanalysis from './Chargdataanalysis';
import Chargtransactionstatistics from './Chargtransactionstatistics';
import censusinfo from './censusinfo'
export default {
    name:'Cgdataanalysis',
    data(){
        return{
            myChart:'',
            xData:'',
        }
    },
    components:{
        EchartsMap,
        Chargtransactionstatistics,
        Chargdataanalysis,
        censusinfo
    },
    mounted(){
        // console.log(this.$store.state.stationId)
    },
    methods:{
        // goHome(){
        //     this.$router.push('/Home')
        // },
    },
}
</script>
<style scoped>
.wrap-app{
    width: 100%;
    height: 100%;
}
.wrap{
    width: 1920px;
    height: 1080px;
    overflow: hidden;
    background:url(../../static/daping/img/bg-01.jpg) center no-repeat;
    background-size: 100% 100%;
}
.fl{
    float: left;
}
.clear{
    overflow: hidden;
}
.e-header{
    width: 100%;
    height: 85px;
    background: url(../../static/daping/img/bg-08.png) center no-repeat;
    background-size: 100% 100%;
    margin-bottom: 10px;
}
.e-header .logo{
    width: 431px;
    height: 34px;
    background-size: 100% 100%;
    margin-top: 20px;
    margin-right: 2%;
    cursor: pointer;
}
.line-bar{
    padding: 0 40px 36px;
    width: 100%;
    box-sizing: border-box;
    position: absolute;
    bottom: 0px;
    left: 0;
}
.wrap-echarts{
    position: relative;
    height: 995px;
}
.right-info{
    width: 49%;
    height: 580px;
    padding-right: 40px;
    box-sizing: border-box;
    position: absolute;
    right: 0;
    top: 0;
}

.header-btn .btn-list{
    width: 231px;
    height: 52px;
    line-height: 48px;
    color: #ffffff;
    background: url(../../static/daping/img/btn-03.png) center no-repeat;
    background-size: 100% 100%;
    text-align: center;
    margin-left: -32px;
    cursor: pointer;
    margin-top: 28px;
}
.header-btn .btn-list.on{
    background: url(../../static/daping/img/btn-04.png) center no-repeat;
    background-size: 100% 100%;
}
.header-btn .btn-list.btn-mrg{
    margin-left: 0;
}
.header-btn .btn-bg{
    width: 635px;
    height: 47px;
    background: url(../../static/daping/img/bg-11.png) center no-repeat;
    background-size: 100% 100%;
    margin-left: -32px;
    margin-top: 28px;
}
.btn-bg .carbon{
    padding-left: 58px;
    padding-top: 5px;
    background: url(../../static/daping/img/pic-15.png) center left no-repeat;
    background-size: 42px 37px;
    margin-right: 68px;
}
.btn-bg .carbon.carbon-tree{
    background: url(../../static/daping/img/pic-16.png) center left no-repeat;
    background-size: 38px 37px;
}
.btn-bg .carbon:first-child{
    margin-left: 155px;
}
.btn-bg .carbon span{
    display: block;
}
.btn-bg .carbon span.num{
    font-size: 18px;
    color: #ffffff;
    line-height: 18px;
    text-align:left;
}
.btn-bg .carbon span.text{
    font-size: 14px;
    color: #88d5ff;
    line-height: 20px;
}
@media screen and (min-width:1920px){
    .wrap-app{
        overflow-x: hidden;
    }
}
</style>