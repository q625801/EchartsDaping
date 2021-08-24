<template>
    <div class="fl charg-linebar">
        <div class="bt">XXXXXXX</div>
        <div class="charg-analysis">
            <div class="wrap-analysis">
                <!-- <div class="analysis-btn" v-if="!stationId">
                    <span :class="analysisbtnType == 0 ? 'on' : ''" @click="getChargingData(0)">XXXXX</span>
                    <span :class="analysisbtnType == 1 ? 'on' : ''" @click="getChargingData(1)">XXXXX</span>
                    <span :class="analysisbtnType == 2 ? 'on' : ''" @click="getChargingData(2)">XXXXX</span>
                </div> -->
                <div class="analysis-two">
                    <div class="single-shot">
                         <!-- <div class="single-icon"></div> -->
                        <span class="num">{{utilizationAverage}}%</span>
                        <span class="analysis-text">XXXXXXX</span>
                    </div>
                    <div class="single-shot">
                         <!-- <div class="dailycharge-icon"></div> -->
                        <span class="num">{{averageChargingCapacity}}</span>
                        <span class="analysis-text">XXXXXXX<em></em></span>
                    </div>
                </div>
                <div class="echarts-analysis" id="Cgdataanalysis" style="width:82%;height:250px"></div>
            </div>
        </div>
    </div>
</template>
<script>
import * as echarts from 'echarts';
// import utils from 'src/utils/utils';
export default {
    name:'Cgdataanalysis',
    data(){
        return{
            utilizationAverage:'',
            averageChargingCapacity:'',
            analysisbtnType:0,
            stationId:'',
        }
    },
    mounted(){
        this.getChargingData(0);
        console.log(this.getXDay(30))
    },
    methods:{
        getChargingData(type){
            let that = this;
            this.analysisbtnType = type;
            let data = [
                    {
                        date:'2021-05-01',
                        stationId:'xxx',
                        type:0,
                        utilization:'20',
                        averageCharging:50,
                    },
                    {
                        date:'2021-05-02',
                        stationId:'xxx',
                        type:0,
                        utilization:'2.5',
                        averageCharging:100,
                    },
                    {
                        date:'2021-05-03',
                        stationId:'xxx',
                        type:0,
                        utilization:'50',
                        averageCharging:90,
                    },
                    {
                        date:'2021-05-04',
                        stationId:'xxx',
                        type:0,
                        utilization:'40',
                        averageCharging:60,
                    },
                    {
                        date:'2021-05-05',
                        stationId:'xxx',
                        type:0,
                        utilization:'30',
                        averageCharging:70,
                    },
                    {
                        date:'2021-05-06',
                        stationId:'xxx',
                        type:0,
                        utilization:'10',
                        averageCharging:40,
                    },
                    {
                        date:'2021-05-07',
                        stationId:'xxx',
                        type:0,
                        utilization:'10',
                        averageCharging:40,
                    },
                    {
                        date:'2021-05-08',
                        stationId:'xxx',
                        type:0,
                        utilization:'10',
                        averageCharging:40,
                    },
                    {
                        date:'2021-05-09',
                        stationId:'xxx',
                        type:0,
                        utilization:'10',
                        averageCharging:40,
                    },
                    {
                        date:'2021-05-10',
                        stationId:'xxx',
                        type:0,
                        utilization:'10',
                        averageCharging:40,
                    },
            ]
            let xData = [];
            let utilizationArr = [];
            let averageChargingArr = [];
            let tooltipxData = [];
            data.forEach((item,index) => {
                if(item.date.split('-')[2]){
                    if(item.date.split('-')[2] < 10){
                        xData.push(parseInt(item.date.split('-')[2]));
                    }else{
                        xData.push(item.date.split('-')[2]);
                    }
                }
                tooltipxData.push(item.date)
                utilizationArr.push(item.utilization)
                averageChargingArr.push(item.averageCharging)
            })
            this.utilizationAverage = utilizationArr[utilizationArr.length - 1]
            this.averageChargingCapacity = averageChargingArr[averageChargingArr.length - 1]
            that.lineDraw(xData,utilizationArr,averageChargingArr,tooltipxData)
        },
        lineDraw(xData,utilization,averageCharging,tooltipxData){
             //初始化ehcharts实例
            let myChartanalysis=echarts.init(document.getElementById("Cgdataanalysis"));
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
                        let result = ''
                        let bgcolor = ''
                    　　params.forEach(function (item,index) {
                            let unit = '度'
                            if(item.seriesName == '甲'){
                                bgcolor = "#2f94fa"
                                
                            }else if(item.seriesName == '乙'){
                                bgcolor = "#ffad33"
                                unit = "%"
                            }
                            if(index == 0){
                                result += `<span style="display:block;text-align: left;font-size:12px;">${tooltipxData[item.dataIndex]}</span>`
                            }
                    　　　　result += `<div style="overflow:hidden;display:flex;">
                            <div style="overflow:hidden;">
                            <span style="width:10px;height:2px;background-color:${bgcolor};display:block;float:left;margin-top:10px"></span>
                            <span style="display:block;float:left;width:70px;text-align: left;padding-left:10px;box-sizing:border-box;color:#88d5ff;font-size:12px">${item.seriesName}</span>
                            </div>
                            <span style="display:block;float:left;text-align: right;color:#88d5ff;font-size:12px;padding-right:12px;width:55px;">${item.data}${unit}</span>
                            </div>`
                    　　})
                    　　return result
                    }
                },
                grid: {
                    left: "4%",
                    top: "17%",
                    right: "5%",
                    bottom: "14%"
                },
                legend: [
                    {
                        itemWidth: 20,
                        itemHeight: 10,
                        data: [{
                            name: '甲',
                            icon: 'rect', // 用矩形替换
                            itemStyle:{
                                color:'#2f94fa'
                            }
                        }],
                        top: "-2%",
                        right:"32%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 14
                        }
                    },
                    {
                        itemWidth: 20,
                        itemHeight: 2,
                        data: [{
                            name: '乙',
                            icon: 'rect', // 用矩形替换
                            itemStyle:{
                                color:'#ffad33'
                            }
                        }],
                        top: "-2%",
                        right:"15%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 14
                        }
                    }
                ],
                xAxis: {
                    data: xData,
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
                        name: "度",
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
                    {
                        type: "value",
                        name: "%",
                        nameTextStyle: {
                            color: "#2f7fd5",
                            fontSize: 12
                        },
                        position: "right",
                        splitLine: {
                            show: false
                        },
                        axisTick: {
                            show: false
                        },
                        axisLine: {
                            show: false,
                            lineStyle: {
                                color: "#396A87",
                                width: 2
                            }
                        },
                        axisLabel: {
                            show: true,
                            formatter: "{value}", //右侧Y轴文字显示
                            textStyle: {
                                color: "#2f7fd5",
                                fontSize: 12
                            }
                        }
                    }
                ],
                series: [{
                        name: "甲",
                        type: "bar",
                        barWidth: 15,
                        itemStyle: {
                            normal: {
                                color: "rgb(47,149,250)",
                            }
                        },
                        data: averageCharging,
                    },

                    {
                        name: "乙",
                        type: "line",
                        smooth: true,
                        yAxisIndex: 1, //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
                        symbol: 'none', //标记的图形为实心圆
                        lineStyle: {
                            color: "rgb(250,174,48)",
                            width: 2,
                        },
                        data: utilization
                    }
                ]
            }
            //使用刚刚指定的配置项和数据项显示图表
            myChartanalysis.setOption(option);
        },
        getXDay(day){
            var date1 = new Date();
            var date2 = new Date(date1);
            date2.setDate(date1.getDate() - day);
            var agoDay = `${date2.getFullYear()}-${date2.getMonth() + 1<10?`0${date2.getMonth() + 1}`:date2.getMonth() + 1}-${date2.getDate()}`;
            
            var nowDay = `${date1.getFullYear()}-${date1.getMonth() + 1<10?`0${date1.getMonth() + 1}`:date1.getMonth() + 1}-${date1.getDate()}`;
            return {agoDay:agoDay,nowDay:nowDay}
        }
    },
    // computed: {
    //     stationInfo() {
    //         return this.$store.state.stationInfo
    //     }
    // },
    // watch:{
    //     stationInfo:{
    //         handler(newdata,olddata){
    //             this.stationId = newdata.stationId
    //         },
    //         deep:true
    //     }
    // }
}
</script>
<style scoped>
.fl{
    float: left;
}
.charg-linebar{
    width: 50%;
}
.charg-analysis{
    width: 100%;
    box-sizing: border-box;
    padding-right: 10px;
    height: 300px;
}
.wrap-analysis{
    border: 1px solid #004d9f;
    height: 100%;
    background: url(../../static/daping/img/bg-02.png) center no-repeat;
    background-size: 100% 100%;
    position: relative;
}
.wrap-analysis .echarts-analysis{
    position: absolute;
    right: 0;
    bottom: 0;
    padding: 0 10px;
}
.charg-linebar .bt{
    font-size: 16px;
    color: #ffffff;
    text-align: left;
    margin-bottom: 10px;
    width: 310px;
    background: url(../../static/daping/img/pic-01.png) center right no-repeat;
}
.analysis-two{
    width: 128px;
    position: absolute;
    left: 22px;
    bottom: 25px;
}
.single-shot{
    margin-top: 15px;
}
.single-shot .single-icon{
    width: 63px;
    height: 51px;
    background: url(../../static/daping/img/pic-02.png) center no-repeat;
    background-size: 100%;
}
.single-shot .dailycharge-icon{
    width: 63px;
    height: 51px;
    background: url(../../static/daping/img/pic-03.png) center no-repeat;
    background-size: 100%;
}
.single-shot span{
    display: block;
    padding-left: 8px;
}
.single-shot span.num{
    color: #ffffff;
    text-align: left;
    padding: 3px 0 3px 8px;
    font-size: 18px;
}
.single-shot span.analysis-text{
    color:#88d5ff;
    text-align: left;
    font-size: 14px;
}
.single-shot span.analysis-text em{
    font-size: 12px;
    color: #88d5ff;
    font-style: normal;
    padding-left: 7px;
}
.analysis-btn{
    position: absolute;
    top: 17px;
    left: 17px;
}
.analysis-btn span{
    width: 88px;
    height: 32px;
    display: inline-block;
    color: #ffffff;
    background: #006bd8;
    line-height: 32px;
    border-radius: 5px;
    margin-right: 10px;
    font-size: 14px;
    cursor: pointer;
    text-align: center;
}
.analysis-btn span.on{
    background:url(../../static/daping/img/btn-01.png) center no-repeat;
}
.analysis-btn span:hover{
    background:url(../../static/daping/img/btn-01.png) center no-repeat;
}
</style>