<template>
    <div class="fl charg-linebar">
        <div class="bt">XXXX</div>
        <div class="charg-analysis">
            <div class="wrap-analysis">
                <!-- <div class="analysis-btn" v-if="!stationId">
                    <span :class="analysisbtnType == 0 ? 'on' : ''" @click="getChargingData(0)">XXXX</span>
                    <span :class="analysisbtnType == 1 ? 'on' : ''" @click="getChargingData(1)">XXXX</span>
                    <span :class="analysisbtnType == 2 ? 'on' : ''" @click="getChargingData(2)">XXXX</span>
                </div> -->
                <div class="analysis-two">
                    <div class="single-shot">
                        <span class="num">23.45%</span>
                        <span class="analysis-text">XXXX<em></em></span>
                    </div>
                    <div class="single-shot">
                        <span class="num">2311.45</span>
                        <span class="analysis-text">XXXX<em></em></span>
                    </div>
                    <div class="single-shot">
                        <span class="num">2311.45</span>
                        <span class="analysis-text">XXXX<em></em></span>
                    </div>
                </div>
                <div class="echarts-analysis" id="Chargtransactionstatistics" style="width:82%;height:250px"></div>
            </div>
        </div>
    </div>
</template>
<script>
import * as echarts from 'echarts';
export default {
    name:'Chargtransactionstatistics',
    data(){
        return{
            myChart:'',
            xData:[],
            SPLIT_NUMBER:5,
            analysisbtnType:0,
            stationId:'',
        }
    },
    mounted(){
        this.getChargingData(0);
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
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-02',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'4.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-03',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-04',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-05',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-06',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-07',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:300,
                        electricCharge:50,
                        serviceCharge:220,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-08',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-09',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:'20',
                        electricCharge:50,
                        serviceCharge:20,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
                    {
                        date:'2021-05-10',
                        stationId:'xxx',
                        type:0,
                        electricQuantity:100,
                        electricCharge:50,
                        serviceCharge:120,
                        Quantitysequential:'3.4',
                        Chargesequential:'2.2',
                        serviceChargeequential:'-1.2'
                    },
            ]
            let xData = [];
            let electricQuantityArr = [];
            let electricChargeArr = [];
            let serviceChargeArr = [];
            let QuantitysequentialArr = [];
            let ChargesequentialArr = [];
            let serviceChargeequentialArr = [];
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
                electricQuantityArr.push(item.electricQuantity)
                electricChargeArr.push(item.electricCharge)
                serviceChargeArr.push(item.serviceCharge)
                //环比
                QuantitysequentialArr.push(item.Quantitysequential)
                ChargesequentialArr.push(item.Chargesequential)
                serviceChargeequentialArr.push(item.serviceChargeequential)
            })
            let rightmax = [],leftmax = [];
            rightmax.push(Math.max(...electricChargeArr))
            rightmax.push(Math.max(...serviceChargeArr))
            rightmax = Math.max(...rightmax)

            leftmax = Math.max(...electricQuantityArr)
            console.log(rightmax,leftmax)
            that.lineDraw(xData,electricQuantityArr,electricChargeArr,serviceChargeArr,QuantitysequentialArr,ChargesequentialArr,serviceChargeequentialArr,tooltipxData,rightmax,leftmax)
        },
        lineDraw(xData,electricQuantityArr,electricChargeArr,serviceChargeArr,QuantitysequentialArr,ChargesequentialArr,serviceChargeequentialArr,tooltipxData,rightmax,leftmax){
            let that = this
             //初始化ehcharts实例
            let myChart=echarts.init(document.getElementById("Chargtransactionstatistics"));
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
                        lineStyle: {
                            width: 2,
                            type:'solid',
                            color:'#225ca6'
                        }
                    },
                    formatter:function(params){
                        let result = ''
                        let bgcolor = ''
                        let equential = ''
                    　　params.forEach(function (item,index) {
                            let unit = '元'
                            if(item.seriesName == '甲'){
                                bgcolor = "#2f94fa"
                                unit = "度"
                            }else if(item.seriesName == '乙'){
                                bgcolor = "#00feff"
                            }else if(item.seriesName == '丙'){
                                bgcolor = "#f2ad23"
                            }
                            switch (index) {
                                case 0:
                                    equential = QuantitysequentialArr[item.dataIndex]
                                    break;
                                case 1:
                                    equential = ChargesequentialArr[item.dataIndex]
                                    break;
                                case 2:
                                    equential = serviceChargeequentialArr[item.dataIndex]
                                    break;
                                default:
                                    break;
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
                            <span style="display:block;float:left;text-algin:right;font-size:12px;color:#88d5ff;">环比</span>
                            <span style="color:${equential > 0 ? '#ff6868' : '#73e833'};font-style:normal;font-size:12px;padding-left:6px">${equential > 0 ? `+${equential}%` : `${equential}%`}</span>
                        </div>`
                    　　})
                    　　return result
                    }
                },
                grid: {
                    left: "5%",
                    top: "15%",
                    right: "5%",
                    bottom: "15%"
                },
                legend: [
                    {
                        itemWidth: 20,
                        itemHeight: 2,
                        data: [{
                            name: '甲',
                            icon: 'rect',
                            itemStyle:{
                                color:'#3196fa'
                            }
                        }],
                        top: "0%",
                        right:"40%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 12
                        }
                    },
                    {
                        itemWidth: 20,
                        itemHeight: 2,
                        data: [{
                            name: '乙',
                            icon: 'rect',
                            itemStyle:{
                                color:'#00feff'
                            }
                        }],
                        top: "0%",
                        right:"26%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 12
                        }
                    },
                    {
                        itemWidth: 20,
                        itemHeight: 2,
                        data: [{
                            name: '丙',
                            icon: 'rect',
                            itemStyle:{
                                color:'#ffb31f'
                            }
                        }],
                        top: "0%",
                        right:"11%",
                        textStyle: {
                            color: "#ffffff",
                            fontSize: 12
                        }
                    }
                ],
                xAxis: {
                    data: xData,
                    axisLine: {
                        show: true, //X轴轴线
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
                    },
                    boundaryGap: false
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
                        name: "元",
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
                        type: "line",
                        yAxisIndex: 0, //使用的 y 轴的 index，在单个图表实例中存在多个 y轴的时候有用
                        symbol: 'circle',
                        showSymbol:false,
                        symbolSize:8,
                        smooth: true,
                        lineStyle: {
                            color: '#3196fa',
                        },
                        itemStyle:{ //拐点设置
                            color:'#3196fa',
                        },
                        z:99,
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(49,150,250,0.3)'
                                },
                                {
                                    offset: 1,
                                    color: 'rgba(49,150,250,0)'
                                }
                                ], false),
                                shadowColor: 'rgba(49,150,250, 0.9)',
                                shadowBlur: 20
                            }
                        },
                        data: electricQuantityArr,
                    },
                    {
                        name: "乙",
                        type: 'line',
                        symbol: 'circle',
                        showSymbol:false,
                        symbolSize:8,
                        smooth: true,
                        yAxisIndex: 1,
                        lineStyle: {
                            color: '#00feff'
                        },
                        itemStyle:{ //拐点设置
                            color:'#00feff',
                        },
                        z:97,
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(0,254,255,0.3)'
                                },
                                {
                                    offset: 1,
                                    color: 'rgba(0,254,255,0)'
                                }
                                ], false),
                                shadowColor: 'rgba(0,254,255, 0.9)',
                                shadowBlur: 20
                            }
                        },
                        data: electricChargeArr
                    },
                    {
                        name: "丙",
                        type: 'line',
                        symbol: 'circle',
                        showSymbol:false,
                        symbolSize:8,
                        smooth: true,
                        yAxisIndex: 1,
                        lineStyle: {
                            color: '#f2ad23'
                        },
                        itemStyle:{ //拐点设置
                            color:'#f2ad23',
                        },
                        z:98,
                        areaStyle: {
                            normal: {
                                color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [{
                                    offset: 0,
                                    color: 'rgba(242,173,35,0.3)'
                                },
                                {
                                    offset: 1,
                                    color: 'rgba(242,173,35,0)'
                                }
                                ], false),
                                shadowColor: 'rgba(242,173,35, 0.9)',
                                shadowBlur: 20
                            }
                        },
                        data: serviceChargeArr
                    }
                ]
            }
            console.log(option.yAxis)
            option.yAxis.forEach((y, index) => {
                let max = !index ? leftmax + '' : rightmax + '';
                max = this.computeMax(max);
                y.splitNumber = this.SPLIT_NUMBER;
                y.interval = max / this.SPLIT_NUMBER;
                y.max = max;
            });
            //使用刚刚指定的配置项和数据项显示图表
            myChart.setOption(option);
        },
        computeMax(value) {
            if (Math.floor(value) === 0) {  // 是小数
                let { result, digit } = this.getNumberFromDecimal(Number(value));
                result = result.substr(0, 2);    // 取前两位
                return Number(Math.ceil(value / this.SPLIT_NUMBER) * this.SPLIT_NUMBER) / Math.pow(10, digit - 1 + 2);
            } else {
                const roundValue = Math.floor(value).toString();
                if (roundValue.length > 2) { // 两位以上
                const topTwo = roundValue.substr(0, 2);
                const len = roundValue.length;
                return Number(Math.ceil(topTwo / this.SPLIT_NUMBER) * this.SPLIT_NUMBER) * Math.pow(10, len - 2);
                } else {
                return Number(Math.ceil(value / this.SPLIT_NUMBER) * this.SPLIT_NUMBER);
                }
            }
        },
        getNumberFromDecimal(decimal) {
            let str = decimal.toString();
            if (typeof decimal !== 'number' || !str.includes('.')) {
                throw '参数不是小数';
            }
            if (decimal >= 1) {
                throw '参数大于等于1';
            }
            for (let i = 0; i < str.length; i ++) {
                if (str[i] !== '0' && str[i] !== '.') {
                return { result: str.substring(i, str.length), digit: i - 2 };
                }
            }
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
    padding-left: 10px;
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
    margin-left: 10px;
    margin-bottom: 10px;
    width: 310px;
    background: url(../../static/daping/img/pic-01.png) center right no-repeat;
}
.analysis-two{
    width: 128px;
    position: absolute;
    left: 10px;
    bottom: 35px;
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