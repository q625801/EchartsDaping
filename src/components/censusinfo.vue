<template>
    <div class="census-info clear">
        <div class="wrap-info">
            <div class="info-list fl">
                <div class="info-content">
                    <span class="num"><animate-number from="1" to="355"></animate-number></span>
                    <span class="text">XXX</span>
                </div>
            </div>
            <div class="info-list fl">
                <div class="info-content info-chargingstation">
                    <span class="num"><animate-number from="1" to="355"></animate-number></span>
                    <span class="text">XXX</span>
                </div>
            </div>
            <div class="info-list fl">
                <div class="info-content info-chargingpile">
                    <span class="num"><animate-number from="1" to="355"></animate-number></span>
                    <span class="text">XXX</span>
                </div>
            </div>
            <div class="info-list fl">
                <div class="info-content info-charginggun">
                    <span class="num"><animate-number from="1" to="355"></animate-number></span>
                    <span class="text">XXX</span>
                </div>
            </div>
        </div>
        <div class="census-accessmode fl">
            <div class="bt">XXX</div>
            <div class="accessmode-echarts">
                <div id="accessmode"></div>
                <!--<div class="chargpiebg"></div>-->
                <div class="accessmode-num">
                    <span class="accessmode-span"><animate-number from="1" :to="numanmite"></animate-number><em class="hl">个</em></span>
                    <span class="accessmode-span"><animate-number from="1" to="1355"></animate-number><em class="pt">个</em></span>
                    <span class="accessmode-span"><animate-number from="1" to="2355"></animate-number><em class="hw">个</em></span>
                </div>
            </div>
        </div>
        <div class="credit-statistics fr">
            <div class="info-bt">XXX</div>
            <div class="credit-div">
                <div class="credit-head credit-head-tr clear">
                    <div class="credit-name fl">项目名称</div>
                    <div class="credit-column-1 fl">项目名称</div>
                    <div class="credit-column-2 fl">项目名称</div>
                    <div class="credit-column-3 fl">项目名称</div>
                    <div class="credit-column-4 fl">项目名称</div>
                </div>
                <div class="credit-body">
                    <div class="credit-head credit-body-tr clear">
                        <div class="credit-name fl">项目名称</div>
                        <div class="credit-column-1 fl">161.2</div>
                        <div class="credit-column-2 fl">5</div>
                        <div class="credit-column-3 fl">2.3</div>
                        <div class="credit-column-4 fl">6</div>
                    </div>
                    <div class="credit-head credit-body-tr clear">
                        <div class="credit-name fl">项目名称</div>
                        <div class="credit-column-1 fl">161.2</div>
                        <div class="credit-column-2 fl">5</div>
                        <div class="credit-column-3 fl">2.3</div>
                        <div class="credit-column-4 fl">6</div>
                    </div>
                    <div class="credit-head credit-body-tr clear">
                        <div class="credit-name fl">项目名称</div>
                        <div class="credit-column-1 fl">161.2</div>
                        <div class="credit-column-2 fl">5</div>
                        <div class="credit-column-3 fl">2.3</div>
                        <div class="credit-column-4 fl">6</div>
                    </div>
                    <div class="credit-head credit-body-tr clear">
                        <div class="credit-name fl">项目名称</div>
                        <div class="credit-column-1 fl">161.2</div>
                        <div class="credit-column-2 fl">5</div>
                        <div class="credit-column-3 fl">2.3</div>
                        <div class="credit-column-4 fl">6</div>
                    </div>
                </div>
            </div>
        </div>
        <div class="chargerank fl">
            <div class="info-bt">XXX</div>
            <div class="chargerank-echarts clear">
                <div id="scrollDiv" class="clear">
                    <ul class="chargerank-all">
                        <li class="chargerank-list">
                            <span class="bt">NO.1  XXX  <animate-number from="1" to="100392"></animate-number></span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.2  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.3  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.4  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.5  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.6 XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.7  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.1  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.1  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                        <li class="chargerank-list">
                            <span class="bt">NO.1  XXX  100392</span>
                            <div class="line-bg">
                                <div class="line-color"></div>
                            </div>
                        </li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="cash-statistics fr">
            <div class="info-bt">XXX</div>
            <div class="cashstatistics-div clear">
                <div class="cashstatistics-all fl">
                    <div class="cashstatistics-info">
                        <span class="num">1134.25</span>
                        <span class="unit">元</span>
                        <span class="total">本月合计</span>
                    </div>
                    <div class="cashstatistics-img"></div>
                </div>
                <div id="cashstatistics-echarts" class="fr"></div>
            </div>
        </div>
    </div>
</template>
<script>
import * as echarts from 'echarts';
import $ from "jquery";
import '../../static/daping/js/jq_scroll.js';
export default {
    name:'basicinfo',
    data(){
        return{
            stationId:'',
            numanmite:155555,
            tableData: [{
            name: '王小虎',
            address: '5'
          }]
        }
    },
    mounted(){
        this.pieDraw();
        this.barhDraw();
        this.cashstatisticsDraw();
        $("#scrollDiv").Scroll({line:1,speed:500,timer:5000,up:"but_up",down:"but_down"});
    },
    methods:{
        pieDraw(){
             //初始化ehcharts实例
            let colorList = ['#00fbff','#008aff','#ffc000']
            let mdata = ['123','200','3000000']
            let myChart=echarts.init(document.getElementById("accessmode"));
            let option = {
                tooltip: {
                    trigger: "item",
                    backgroundColor:"rgb(19,82,153)",
                    borderWidth:0,
                    textStyle:{
                        color:"#ffffff",
                    },
                    extraCssText: 'box-shadow: 0 0 10px rgba(0, 9, 41, 0.8)',
                    axisPointer: {
                        type: "shadow",
                        label: {
                            show: false
                        },
                        shadowStyle:{
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(49,150,250,0.3)'
                                },
                                {
                                    offset: 1,
                                    color: 'rgba(49,150,250,0)'
                                }
                            ], false),
                        }
                    },
                },
                legend: {
                    backgroundColor:'transparent',
                    orient: 'vertical',
                    padding:15,
                    itemGap:15,
                    itemWidth:8,
                    right:'25%',
                    bottom:'23%',
                    textStyle:{
                        fontSize:14,
                        padding: [0, 0, 0, 6]
                        // align:'right',
                        // rich:{
                        //     a:{
                        //         fontSize:14,
                        //         // verticalAlign:'top',
                        //         align:'center',
                        //         padding:[0,0,0,11],
                        //         lineHeight:13,
                        //     },
                        //     b:{
                        //         align: 'right',
                        //         // width: 70,
                        //         fontSize:16,
                        //         color:'#ffffff',
                        //         padding:[0,0,0,0],
                        //         // verticalAlign:'top',
                        //     },
                        //     c:{
                        //         fontSize:14,
                        //         padding:[0,0,0,0],
                        //         verticalAlign:'top',
                        //         align:'left',
                        //         // width:0,
                        //     }
                        // }
                    },
                    // formatter:  (name)=>{
                    //     let num
                    //     switch (name) {
                    //         case '互联互通':
                    //             num = mdata[0]
                    //             break;
                    //         case '平台直连':
                    //             num = mdata[1]
                    //             break;
                    //         case '红外接入':
                    //             num = mdata[2]
                    //             break;
                    //         default:
                    //             break;
                    //     }
                    //     let arr = [
                    //         '{a|'+name+'}{b|' + num + '}{c|个}',
                    //     ]
                    //     return arr.join('\n')
                    // },
                    data: [
                        {
                            name: '甲',
                            // 强制设置图形为圆。
                            icon: 'circle',
                            // 设置文本为红色
                            textStyle: {
                                color: '#00fbff'
                            },
                            itemStyle:{
                                borderWidth: 6, // 区域边框宽度
                                borderColor: "rgba(0,251,255,0.3)", // 区域边框颜色
                            },
                        },
                        {
                            name: '乙',
                            // 强制设置图形为圆。
                            icon: 'circle',
                            // 设置文本为红色
                            textStyle: {
                                color: '#008aff'
                            },
                            itemStyle:{
                                borderWidth: 6, // 区域边框宽度
                                borderColor: "rgba(0,138,255,0.3)", // 区域边框颜色
                            },
                        },
                        {
                            name: '丙',
                            // 强制设置图形为圆。
                            icon: 'circle',
                            // 设置文本为红色
                            textStyle: {
                                color: '#ffc000'
                            },
                            itemStyle:{
                                borderWidth: 6, // 区域边框宽度
                                borderColor: "rgba(255,192,0,0.3)", // 区域边框颜色
                            },
                        }
                    ],
                    
                },
                series: [
                    {
                        name: '甲乙丙',
                        type: 'pie',
                        left: "-43%",
                        radius: ['50%', '62%'],
                        avoidLabelOverlap: false,
                        label: {
                            show: false,
                            position: 'center',
                        },
                        emphasis: {
                            label: {
                                show: false,
                            },
                        },
                        labelLine: {
                            show: false,
                        },
                        itemStyle:{
                            normal: {
                                borderColor:'#02164e',
                                borderWidth:'2',
                                color: (params) => {
                                    return colorList[params.dataIndex]
                                }
                            },
                            
                        },
                        data: [
                            { value: 580, name: '甲' },
                            { value: 484, name: '乙' },
                            { value: 300, name: '丙' },
                        ],
                    },
                ],
            };
            myChart.setOption(option);
        },
        barhDraw(){
            
        },
        cashstatisticsDraw(){
             //初始化ehcharts实例
            let myChartanalysis=echarts.init(document.getElementById("cashstatistics-echarts"));
            //指定图表的配置项和数据
            var option = {
                backgroundColor: 'transparent',
                tooltip: {
                    trigger: "axis",
                    backgroundColor:"rgb(19,82,153)",
                    borderWidth:0,
                    textStyle:{
                        color:"#ffffff",
                    },
                    extraCssText: 'box-shadow: 0 0 10px rgba(0, 9, 41, 0.8)',
                    axisPointer: {
                        type: "shadow",
                        label: {
                            show: false
                        },
                        shadowStyle:{
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(49,150,250,0.3)'
                                },
                                {
                                    offset: 1,
                                    color: 'rgba(49,150,250,0)'
                                }
                            ], false),
                        }
                    },
                    formatter:function(params){
                        console.log(params)
                        let result = '';
                        let color = '';
                        params.forEach(function (item,index) {
                            if(index == 0){
                                result += `<span style="display:block;text-align: left;font-size:12px;">${item.axisValue}</span>`
                            }
                            result += `<div style="display:flex;align-items: center;"><span style="width:6px;height:6px;background-color:${item.color};display:inline-block;margin-right:5px"></span><span style="color:#88d5ff;font-size:12px;">${item.seriesName}<span><span style="font-size:12px;padding-left:28px;color:#88d5ff">${item.value}</span></div>`
                    　　})
                    　　return result
                    },
                },
                grid: {
                    left: "10%",
                    top: "17%",
                    right: "5%",
                    bottom: "25%"
                },
                xAxis: {
                    data: [
                        "00:00",
                        "02:00",
                        "04:00",
                        "06:00",
                        "08:00",
                    ],
                    axisLine: {
                        show: true, //隐藏X轴轴线
                        lineStyle: {
                            color: "#7c8798",
                            width: 1
                        }
                    },
                    axisTick: {
                        show: false, //隐藏X轴刻度
                        alignWithLabel: true
                    },
                    axisLabel: {
                        show: true,
                        textStyle: {
                            color: "#2f7fd5", //X轴文字颜色
                            fontSize: 12
                        },
                        interval: 0,
                    }
                },
                yAxis: [{
                        type: "value",
                        name: "个",
                        nameTextStyle: {
                            color: "#2f7fd5",
                            fontSize: 12
                        },
                        splitLine: {
                            show: true,
                            lineStyle: {
                                type:'dashed',
                                width: 1,
                                color: "#394971" //横轴线条颜色
                            }
                        },
                        axisTick: {
                            show: false
                        },
                        axisLine: {
                            show: false
                        },
                        axisLabel: {
                            show: true,
                            textStyle: {
                                color: "#2f7fd5",
                                fontSize: 12
                            }
                        }
                    },
                ],
                series: [{
                        name: "2021.04",
                        type: "bar",
                        barWidth: 10,
                        barGap: '0%',
                        itemStyle: {
                            normal: {
                                color: "rgb(47,148,250)",
                            }
                        },
                        data: [24, 45, 43, 35, 76]
                    },

                    {
                        name: "2020.04",
                        type: "bar",
                        smooth: true,
                        barWidth: 10,
                        itemStyle: {
                            normal: {
                                color: "rgb(0,254,255)",
                            }
                        },
                        data: [20, 40,60, 80, 100]
                    }
                ]
            }
            //使用刚刚指定的配置项和数据项显示图表
            myChartanalysis.setOption(option);
        }
    },
    computed: {
        // stationInfo() {
        //     return this.$store.state.stationInfo
        // }
    },
    watch:{
        // stationInfo:{
        //     handler(newdata,olddata){
        //         this.stationId = newdata.stationId
        //     },
        //     deep:true
        // }
    }
}
</script>
<style scoped>
.fl{
    float: left;
}
.fr{
    float: right;
}
.clear{
    overflow: hidden;
}
.census-info{
    padding-top: 14px;
}
.census-accessmode{
    width: 45%;
}
.census-accessmode .bt{
    font-size: 16px;
    color: #ffffff;
    padding-left: 14px;
    background: url(../../static/daping/img/line-02.png) center left no-repeat;
    background-size: 5px 13px;
    text-align: left;
}
.accessmode-echarts{
    width: 100%;
    height: 195px;
    background: url(../../static/daping/img/bg-06.png) center no-repeat;
    background-size: 100% 100%;
    margin-top: 8px;
    position: relative;
}
#accessmode{
    width:100%;
    height:195px;
    position: relative;
    z-index: 99;
}
.chargpiebg{
    position: absolute;
    left:16.35%;
    top: 24.5%;
    width: 99px;
    height: 98px;
    background: url(../../static/daping/img/pic-11.png) center no-repeat;
    background-size: 100%;
}
.accessmode-num{
    position: absolute;
    top: 30%;
    right: 9%;
}
.accessmode-num .accessmode-span{
    display: block;
    text-align: right;
    color: #ffffff;
    font-size: 16px;
    padding-bottom: 11px;
}
.accessmode-num .accessmode-span em{
    font-style: normal;
    font-size: 14px;
    padding-left: 5px;
}
.accessmode-num .accessmode-span em.hl{
    color: #00fbff;
}
.accessmode-num .accessmode-span em.pt{
    color: #0089ff;
}
.accessmode-num .accessmode-span em.hw{
    color: #fbc004;
}
.credit-statistics{
    width: 51%;
}
.info-bt{
    font-size: 16px;
    color: #ffffff;
    background:url(../../static/daping/img/pic-10.png) 111px center no-repeat;
    background-size: 374px 16px;
    text-align: left;
}
.credit-div{
    width: 100%;
    height: 195px;
    box-sizing: border-box;
    padding: 10px 5px;
    background: url(../../static/daping/img/bg-07.png) center no-repeat;
    background-size: 100% 100%;
    margin-top: 8px;
    position: relative;
}
.credit-head{
    padding: 5px 10px 5px 22px;
    background: #0b4690;
}
.credit-head div{
    font-size: 14px;
    color: #78a8e2;
    margin-right: 20px;
    text-align: center;
}
.credit-head div:last-child{
    margin-right: 0;
}
.credit-head div.credit-name{
    width: calc(100% - 310px);
    margin-right: 0;
    text-align: left;
    height: 38px;
    line-height: 38px;
}
.credit-head-tr div{
    height: 38px;
    line-height: 38px;
}
.credit-head div.credit-column-1,.credit-head div.credit-column-3,.credit-head div.credit-column-4{
    width: 60px;
}
.credit-head div.credit-column-2{
    width: 70px;
}
.credit-body-tr{
    background: rgba(11, 70, 144, 0.2);
    padding: 0 10px 0 22px;
}
.credit-body-tr:nth-child(2n){
    background: rgba(11, 70, 144, 0.6);
}
.credit-body-tr div{
    line-height: 32px;
}
.credit-body-tr div.credit-name{
    height: 32px;
    line-height: 32px;
}
.chargerank{
    width: 45%;
    margin-top: 22px;
}
.chargerank .info-bt{
    background:url(../../static/daping/img/pic-10.png) 200px center no-repeat;
    background-size: 300px 16px;
}
.chargerank-echarts{
    width: 100%;
    height: 195px;
    background: url(../../static/daping/img/bg-06.png) center no-repeat;
    background-size: 100% 100%;
    margin-top: 8px;
    position: relative;
    padding: 10px 43px 16px 32px;
    box-sizing: border-box;
}
#chargerank-echarts{
    width:100%;
    height:195px;
    position: relative;
    z-index: 99;
}
.cash-statistics{
    width: 51%;
    margin-top: 22px;
}
.cash-statistics .info-bt{
    background:url(../../static/daping/img/pic-10.png) 140px center no-repeat;
    background-size: 374px 16px;
}
.cashstatistics-div{
    width: 100%;
    height: 195px;
    box-sizing: border-box;
    padding: 10px;
    background: url(../../static/daping/img/bg-07.png) center no-repeat;
    background-size: 100% 100%;
    margin-top: 8px;
    position: relative;
}
#cashstatistics-echarts{
    width: 75%;
    height: 195px;
}
.cashstatistics-all{
    width: 21%;
    height: 170px;
    box-sizing: border-box;
    background-color: #094897;
    padding: 15px 10px;
}
.cashstatistics-info{
    padding-bottom: 8px;
    border-bottom: 1px solid #3c82c2;
}
.cashstatistics-info span{
    display: block;
    text-align: left;
}
.cashstatistics-info .num{
    font-size: 18px;
    color: #ffffff;
    padding-bottom: 10px;
}
.cashstatistics-info .unit{
    font-size: 12px;
    color: #88d5ff;
    padding-bottom: 5px;
}
.cashstatistics-info .total{
    font-size: 14px;
    color: #88d5ff;
}
.cashstatistics-img{
    width: 50px;
    height: 50px;
    margin-top: 10px;
    background: url(../../static/daping/img/pic-12.png) center no-repeat;
    background-size: 100%;
    margin-left: 0px;
}
.chargerank-all{
    width: 100%;
    height: 100%;
}
.chargerank-list{
    margin-bottom: 5px;
}
.chargerank-list span.bt{
    font-size: 14px;
    color: #88d5ff;
    display: block;
    text-align:left;
}
.chargerank-list .line-bg{
    width: 100%;
    height: 8px;
    margin-top: 2px;
    background: rgba(49,150,250,0.1);
    border-radius: 0 30px 30px 0;
}
.chargerank-list .line-bg .line-color{
    background: #fd6363;
    width: 80%;
    height: 100%;
    border-radius: 0 30px 30px 0;
}
#scrollDiv{
    width: 100%;
    height: 100%;
}
.wrap-info{
    width: 100%;
    height: 101px;
    background: url(../../static/daping/img/bg-05.png) center no-repeat;
    background-size: 100%;
    overflow: hidden;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    margin-bottom: 15px;
}
.info-list{
    padding-top: 20px;
    padding-left: 30px;
    background: url(../../static/daping/img/line-01.png) center right no-repeat;
    background-size: 3px 27px;
    padding-right: 92px;
}
.info-list:last-child{
    padding-right: 32px;
    background:none;
}
.info-content{
    padding: 10px 0 10px 50px;
    background: url(../../static/daping/img/pic-06.png) center left no-repeat;
    background-size: 40px;
}
.info-content span{
    display: block;
}
.info-content span.num{
    font-size: 18px;
    color: #e99e32;
    text-align: left;
}
.info-content span.text{
    font-size:14px;
    color:#88d5ff
}
.info-chargingstation{
    background: url(../../static/daping/img/pic-07.png) center left no-repeat;
    background-size: 40px;
    padding: 10px 0 10px 40px;
}
.info-chargingpile{
    background: url(../../static/daping/img/pic-08.png) center left no-repeat;
    background-size: 40px;
    padding: 11px 0 11px 50px;
}
.info-charginggun{
    background: url(../../static/daping/img/pic-09.png) center left no-repeat;
    background-size: 40px;
    padding: 10px 0 10px 50px;
}

</style>
