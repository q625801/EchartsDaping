<template>
    <div class="wrap-map">
        <div style="width:100%;position:absolute;z-index:999">
            <div id="myChart" style="width:100%;height:680px;margin:0 auto;transform: rotate3d(1, 0, 0, 25deg);"></div>
        </div>
        <div class="echarts-map"></div>
        <!-- <div ref="viewC" class="map-nav" v-show="!viewChina">
           <span>全国站点总览</span>
        </div> -->
        <div class="rhoaias">
            <div class="rhoaias-one"></div>
            <div class="rhoaias-two"></div>
            <div class="rhoaias-three"></div>
        </div>
        <div class="overviewdata" ref="viewChina" v-show="viewChina"></div>
    </div>
  
</template>

<script>
import * as echarts from 'echarts';
import '../../static/daping/js/china.js'
import regionColor from '../../static/daping/js/region.js'
import Bg from '../../static/daping/img/bg-03.png'
import Bghw from '../../static/daping/img/bg-hw.png'
import Bgptzl from '../../static/daping/img/bg-ptzl.png'
import Pic from '../../static/daping/img/pic-04.png'
import Pic2 from '../../static/daping/img/pic-13.png'
import Pic3 from '../../static/daping/img/pic-14.png'
import Pic4 from '../../static/daping/img/pic-17.png'
import $ from 'jquery';
export default {
  name: 'hello',
  data () {
    return {
      option:'',
      regions:regionColor,
      Bg:Bg,
      Bghw:Bghw,
      Bgptzl:Bgptzl,
      Pic:Pic,
      Pic2:Pic2,
      Pic3:Pic3,
      viewChina:false,
      effectdataIndex:-1,
      effectseriesIndex:-1,
      chinaTimer:'',
      numbar:0,
      numeffectScatter: 1,
      mapType:'china',
      provinceTimer:'',
      provinceseriesIndex:0,
      provincedataIndex:-1
    }
  },
  mounted(){
    this.getMapData();
  },
  methods: {
    lookVideoGo(){
        console.log("1111")
    },
    getMapData(){
        let data= [
            {
                provinceName:'浙江',
                data:[
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 119.5313,
                        lat: 29.8773,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                        stationId:'acascczc',
                    },
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 119.5313,
                        lat: 28.8773,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                        stationId:'acascczc',
                    },
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 119.5313,
                        lat: 29.2773,
                        status:1,
                        stationName:'XXXX',
                        type:1,
                        stationId:'asd1111',
                    },
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 119.5313,
                        lat: 29.0773,
                        status:1,
                        stationName:'XXXX',
                        type:2,
                        stationId:'asd2222',
                    }
                ]
            },
            {
                provinceName:'福建',
                data:[
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 118.0543,
                        lat: 26.0522,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                    },
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 119.5313,
                        lat: 25.8773,
                        status:1,
                        stationName:'XXXX',
                        type:1,
                    },
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 118.5313,
                        lat: 25.0073,
                        status:1,
                        stationName:'XXXX',
                        type:2,
                    }
                ]
            },
            {
                provinceName:'吉林',
                data:[
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 118.0543,
                        lat: 26.0522,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                    },
                ]
            },
            {
                provinceName:'新疆',
                data:[
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 118.0543,
                        lat: 26.0522,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                    },
                ]
            },
            {
                provinceName:'内蒙古',
                data:[
                    {
                        address: '浙江杭州XXXXXXXXxxxxx',
                        lon: 118.0543,
                        lat: 26.0522,
                        status:1,
                        stationName:'XXXX',
                        type:0,
                    },
                ]
            }
        ]
        this.drawMap(data);
    },
    drawMap(data){
        let that = this;
        let myChart=echarts.init(document.getElementById("myChart"));
        let geoCoordMap = {
            '台湾': [121.5135,25.0308],
            '黑龙江': [127.9688, 45.368],
            '内蒙古': [110.3467, 41.4899],
            "吉林": [125.8154, 44.2584],
            '北京市': [116.4551, 40.2539],
            "辽宁": [123.1238, 42.1216],
            "河北": [114.4995, 38.1006],
            "天津": [117.4219, 39.4189],
            "山西": [112.3352, 37.9413],
            "陕西": [109.1162, 34.2004],
            "甘肃": [103.5901, 36.3043],
            "宁夏": [106.3586, 38.1775],
            "青海": [101.4038, 36.8207],
            "新疆": [87.9236, 43.5883],
            "西藏": [91.11, 29.97],
            "四川": [103.9526, 30.7617],
            "重庆": [108.384366, 30.439702],
            "山东": [117.1582, 36.8701],
            "河南": [113.4668, 34.6234],
            "江苏": [118.8062, 31.9208],
            "安徽": [117.29, 32.0581],
            "湖北": [114.3896, 30.6628],
            "浙江": [119.5313, 29.8773],
            "福建": [118.4543, 26.9222],
            "江西": [116.0046, 28.6633],
            "湖南": [113.0823, 28.2568],
            "贵州": [106.6992, 26.7682],
            "云南": [102.9199, 25.4663],
            "广东": [113.12244, 23.009505],
            "广西": [108.479, 23.1152],
            "海南": [110.3893, 19.8516],
            '上海': [121.4648, 31.2891],
        };
        let OverviewArr = [];
        data.forEach((item,index) => {
            let name = item.provinceName;
            let value = geoCoordMap[name].concat(item.data.length)
            OverviewArr.push({name:name,value:value})
        })
        let option = {
            backgroundColor: "transparent",
            geo: [
                {
                    show: true,
                    map: "china",
                    label: {
                        normal: {
                            show: false,
                            color: "#fff"
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    // top:'6%',
                    // left:'13%',
                    layoutCenter: ['50%', '46%'],
                    layoutSize: '105%',
                    roam: false,
                    zoom: 1.1,
                    z:80,
                    animation:false,
                    itemStyle: {
                        normal: {
                            // areaColor:'#1667ab',
                            borderWidth: 1, // 区域边框宽度
                            borderColor: "#49a6e1", // 区域边框颜色
                        },
                        // emphasis: {
                        //     areaColor:'#1667ab',
                        // }
                    },
                    regions: that.regions
                },
                {
                    show: true,
                    map: "china",
                    saspectScale: 0.85,
                    // top:'9%',
                    // left:'13%',
                    layoutCenter: ['50%', '47.8%'],
                    layoutSize: '105%',
                    label: {
                        normal: {
                            show: false,
                            color: "#fff"
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    roam: false,
                    animation: false,
                    zoom: 1.1,
                    itemStyle: {
                        normal: {
                            borderWidth: 2, // 区域边框宽度
                            borderColor: "#15b1ff", // 区域边框颜色
                            opacity:0.5,
                        },
                        
                    },
                    regions: that.regions
                },
                {
                    show: true,
                    map: "china",
                    saspectScale: 0.85,
                    // top:'12%',
                    // left:'13%',
                    layoutCenter: ['50%', '49%'],
                    layoutSize: '105%',
                    label: {
                        normal: {
                            show: false,
                            color: "#fff"
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    roam: false,
                    animation: false,
                    zoom: 1.1,
                    itemStyle: {
                        normal: {
                            borderWidth: 2, // 区域边框宽度
                            borderColor: "#15b1ff", // 区域边框颜色
                            opacity:0.3,
                        },
                        
                    },
                    regions: that.regions
                },
                {
                    show: true,
                    map: "china",
                    saspectScale: 0.85,
                    // top:'15%',
                    // left:'13%',
                    layoutCenter: ['50%', '50%'],
                    layoutSize: '105%',
                    label: {
                        normal: {
                            show: false,
                            color: "#fff"
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    roam: false,
                    animation: false,
                    zoom: 1.1,
                    itemStyle: {
                        normal: {
                            borderWidth: 2, // 区域边框宽度
                            borderColor: "#15b1ff", // 区域边框颜色
                            opacity:0.5,
                        },
                        
                    },
                    regions: that.regions
                },
                {
                    show: true,
                    map: "china",
                    label: {
                        normal: {
                            show: false,
                            color: "#fff"
                        },
                        emphasis: {
                            show: false
                        }
                    },
                    z:79,
                    layoutCenter: ['50%', '46%'],
                    layoutSize: '105%',
                    roam: false,
                    animation: false,
                    zoom: 1.1,
                    itemStyle: {
                        normal: {
                            borderWidth: 6, // 区域边框宽度
                            borderColor: "rgba(59,247,255,0.9)", // 区域边框颜色
                        },
                        
                    },
                    regions: that.regions
                }
            ],
            grid:{
                containLabel:true,
            },
            tooltip:{
                show:true,
                triggerOn: "none",
                backgroundColor:"transparent",
                borderWidth:0,
                padding:0,
                extraCssText: 'box-shadow: 0 0 0px rgba(0, 0, 0, 0)',
                position:(pos, params, dom, rect, size) => {
                    let x = pos[0]
                    let y = pos[1]
                    dom.style.transform = 'translateZ(0)'
                    return [rect.x+15,rect.y-5];
                },
                formatter:(params) => {
                    let result = `<div style="width: 120px;height: 32px;background: url(${Pic4}) center no-repeat;background-size: 100%;text-align:center;line-height:32px;color:#ffffff;font-size:14px">XXXX：${params.value / 100}</div>`
                    return result
                }
            },
            series: [     
                // {
                //     name: 'Overview',
                //     type: 'scatter',
                //     coordinateSystem: 'geo',
                //     symbol: 'pin',
                //     symbolSize: [50,50],
                //     label: {
                //         normal: {
                //             show: true,
                //             textStyle: {
                //                 color: '#fff',
                //                 fontSize: 9,
                //             },
                //             formatter (value){
                //                 return value.data.value[2]
                //             }
                //         }
                //     },
                //     tooltip:{
                //         show:true,
                //         backgroundColor:"transparent",
                //         borderWidth:0,
                //         padding:0,
                //         extraCssText: 'box-shadow: 0 0 0px rgba(0, 0, 0, 0)',
                //         position: function (pos, params, dom, rect, size) {
                //             let x = pos[0]
                //             let y = pos[1]
                //             dom.style.transform = 'translateZ(0)'
                //             return [rect.x+10,rect.y-100];
                //         },
                //         formatter:function(params){
                //             let result = '';
                //             return "<div>11111111</div>"
                //         }
                //     },
                //     itemStyle: {
                //         normal: {
                //             color: '#2f94fa', //标志颜色
                //         }
                //     },
                //     data: OverviewArr,
                //     showEffectOn: 'render',
                //     rippleEffect: {
                //         brushType: 'stroke'
                //     },
                //     hoverAnimation: true,
                //     zlevel: 1
                // },
            ]
        };
        that.option = JSON.parse(JSON.stringify(option))
        myChart.setOption(option);
        // that.$refs.viewC.addEventListener("click",() => {
        //     document.getElementsByClassName('effectScattertooltip')[0].setAttribute('style', 'display:none')
        // })
        myChart.on("click", params => {
            //中国地图散点 柱状图 点击事件
            if(params.componentType === "geo" || (params.componentSubType === "effectScatter" && params.seriesName == "Overview") || (params.componentSubType === "bar")){
                myChart.dispatchAction({
                    type: 'hideTip'
                })
                myChart.dispatchAction({
                    type:'downplay',
                })
                that.effectdataIndex = -1
                that.effectseriesIndex = -1
                let option = myChart.getOption();//获得option对象
                // console.log(option)
                let mapCode = that.checkMap(params.name)
                if(mapCode){
                    $.getJSON(`/echartsdemo/dist/static/mapData/${mapCode}.json`,(res) => {
                        that.viewChina = true
                        echarts.registerMap(mapCode, res);
                        option.series = [];
                        let hwdata = {
                                name: '直接访问',
                                type: 'effectScatter',
                                coordinateSystem: 'geo',
                                rippleEffect: {
                                    brushType: "fill",
                                    scale: 4,
                                },
                                showEffectOn: "emphasis",
                                itemStyle: {
                                    normal: {
                                        color: '#ffc000',
                                        borderWidth:10,
                                        borderColor:'rgba(255,192,0,0.29)',
                                        opacity:1
                                    }
                                },
                                data: [],
                                legendHoverLink: false,
                                z:2000,
                                symbolSize: function(val) {
                                    return 12
                                },
                        }
                        let ptzldata = {
                                name: '联盟广告',
                                type: 'effectScatter',
                                coordinateSystem: 'geo',
                                rippleEffect: {
                                    brushType: "fill",
                                    scale: 4,
                                },
                                showEffectOn: "emphasis",
                                itemStyle: {
                                    normal: {
                                        color: '#58ed2f',
                                        borderWidth:10,
                                        borderColor:'rgba(88,237,47,0.3)',
                                        opacity:1
                                    }
                                },
                                data: [],
                                legendHoverLink: false,
                                z:2000,
                                symbolSize: function(val) {
                                    return 12
                                },                       
                        }
                        let hlhtdata = {
                                name: '视频广告',
                                type: 'effectScatter',
                                coordinateSystem: 'geo',
                                rippleEffect: {
                                    brushType: "fill",
                                    scale: 4
                                },
                                showEffectOn: "emphasis",
                                emphasis: {
                                    // scale: false,
                                    focus: 'none'
                                },
                                itemStyle: {
                                    normal: {
                                        color: '#00fbff',
                                        borderWidth:10,
                                        borderColor:'rgba(0,251,255,0.29)',
                                        opacity:1
                                    }
                                },
                                legendHoverLink: false,
                                data: [],
                                z:2000,
                                symbolSize: function(val) {
                                    return 12
                                },
                        }
                        data.forEach((item,index) =>{
                            if(item.provinceName.indexOf(params.name) >= 0){
                                item.data.forEach((item2,index2) => {
                                    item2.value = [item2.lon,item2.lat]
                                    switch (item2.type) {
                                        case 0:
                                            ptzldata.data.push(item2)
                                            break;
                                        case 1:
                                            hlhtdata.data.push(item2)
                                            break;
                                        case 2:
                                            hwdata.data.push(item2)
                                            break;
                                        default:
                                            break;
                                    }
                                })
                            }
                        })
                        if(hwdata.data.length > 0){
                            option.series.push(hwdata)
                        }
                        if(ptzldata.data.length > 0){
                            option.series.push(ptzldata)
                        }
                        if(hlhtdata.data.length > 0){
                            option.series.push(hlhtdata)
                        }
                        
                        option.tooltip = {
                            show:true,
                            triggerOn: "none",
                            backgroundColor:"transparent",
                            borderWidth:0,
                            padding:0,
                            extraCssText: 'box-shadow: 0 0 0px rgba(0, 0, 0, 0)',
                            position:(pos, params, dom, rect, size) => {
                                let x = pos[0]
                                let y = pos[1]
                                dom.style.transform = 'translateZ(0)'
                                return [rect.x+10,rect.y-100];
                            },
                            formatter:(params) => {
                                let result = '';
                                if(params.componentSubType == "effectScatter" && params.componentType == "series" && params.seriesName != "Overview"){
                                    result += `<div class="effectScattertooltip" style="width:282px;height:145px;box-sizing:border-box;background:url(${params.data.type == 0 ? that.Bgptzl : (params.data.type == 1 ? that.Bg : that.Bghw)}) center no-repeat;padding-top:7px;padding-left:73px;">
                                    <span style="font-size:14px;color:#ffffff;display:block;text-align:left;">${params.data.stationName}</span>
                                    <div style="overflow:hidden;">
                                        <div style="width:90px;height:90px;float:left;margin-top:15px;display:flex;justify-content:center;align-items:center;flex-direction: column;background:url(${params.data.type == 0 ? that.Pic3 : (params.data.type == 1 ? that.Pic : that.Pic2)}) center no-repeat;">
                                        </div>
                                        <div style="float:left;padding-left:18px;padding-top:20px;width:119px;box-sizing: border-box;overflow: hidden;">
                                            <div style="font-size:12px;color:#a5c9e5;text-align:left;line-height: 14px;">状态</div>
                                            <div style="font-size:14px;color:${params.data.type == 0 ? '#4fd32a' : (params.data.type == 1 ? '#4bfefc' : '#ffc000')};text-align:left;padding-bottom:8px;">正常使用</div>
                                            <div style="font-size:12px;color:#a5c9e5;text-align:left;line-height: 14px;">地址</div>
                                            <div style="font-size:14px;color:${params.data.type == 0 ? '#4fd32a' : (params.data.type == 1 ? '#4bfefc' : '#ffc000')};text-align:left;width:100px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">${params.data.address}</div>
                                        </div>
                                    </div></div>`
                                    return result
                                }else{
                                    return result
                                }
                            }
                        };
                        option.legend = {
                            show:false,
                            backgroundColor:'rgba(0,0,0,0.5)',
                            orient: 'vertical',
                            padding:15,
                            borderWidth:2,
                            borderColor:'#0265b0',
                            itemWidth:12,
                            right:'3%',
                            bottom:'10%',
                            textStyle:{
                                rich:{
                                    a:{
                                        fontSize:14,
                                        verticalAlign:'top',
                                        align:'center',
                                        padding:[0,0,0,11],
                                        lineHeight:13,
                                    },
                                }
                            },
                            formatter:  (name)=>{
                                let arr = [
                                    '{a|'+name+'}',
                                ]
                                return arr.join('\n')
                            },
                            data: [
                                {
                                    name: '直接访问',
                                    // 强制设置图形为圆。
                                    icon: 'circle',
                                    // 设置文本为红色
                                    textStyle: {
                                        color: '#ffc000'
                                    },
                                    itemStyle:{
                                        borderWidth: 10, // 区域边框宽度
                                        borderColor: "rgba(255,192,0,0.3)", // 区域边框颜色
                                    },
                                },
                                {
                                    name: '联盟广告',
                                    // 强制设置图形为圆。
                                    icon: 'circle',
                                    // 设置文本为红色
                                    textStyle: {
                                        color: '#58ed2f'
                                    },
                                    itemStyle:{
                                        borderWidth: 10, // 区域边框宽度
                                        borderColor: "rgba(88,237,47,0.3)", // 区域边框颜色
                                    },
                                },
                                {
                                    name: '视频广告',
                                    // 强制设置图形为圆。
                                    icon: 'circle',
                                    // 设置文本为红色
                                    textStyle: {
                                        color: '#00fbff'
                                    },
                                    itemStyle:{
                                        borderWidth: 10, // 区域边框宽度
                                        borderColor: "rgba(0,251,255,0.3)", // 区域边框颜色
                                    },
                                }
                            ],
                        };
                        if(hlhtdata.data.length > 0 || ptzldata.data.length > 0 || hlhtdata.data.length > 0){
                            option.legend.show = true
                        }
                        option.geo.forEach((item,index) => {
                            item.map = mapCode
                            item.itemStyle.areaColor = "#1667ab"
                            item.emphasis.itemStyle.areaColor = "#1667ab"
                            item.zoom = 1
                        })

                        clearInterval(that.chinaTimer)
                        that.chinaTimer = ''
                        that.mapType = 'province'

                        myChart.setOption(option,true);

                        //重置省份定时器数据
                        that.provinceseriesIndex = 0
                        that.provincedataIndex = -1

                        that.Maptolltiptimer(myChart,option)
                    })
                }
            }else if (params.componentType === "series" && params.componentSubType === "effectScatter" && params.seriesName != "Overview") {
                //省份散点点击事件
                let dataIndex = params.dataIndex;
                let seriesIndex = params.seriesIndex;
                if(that.effectdataIndex == dataIndex && that.effectseriesIndex == seriesIndex){
                    return false
                }
                that.effectdataIndex = dataIndex
                that.effectseriesIndex = seriesIndex
                // that.$store.commit('UpdatestationId', params.data);
                myChart.dispatchAction({
                    type:'showTip',
                    seriesIndex: seriesIndex,
                    dataIndex:dataIndex
                })
                myChart.dispatchAction({
                    type:'downplay',
                })
                myChart.dispatchAction({
                    type:'highlight',
                    seriesIndex: seriesIndex,
                    dataIndex:dataIndex
                })
                clearInterval(that.provinceTimer)
                that.provinceTimer = ''
                that.provinceseriesIndex = params.seriesIndex
                that.provincedataIndex = params.dataIndex
            }else{
                that.effectdataIndex = -1
                that.effectseriesIndex = -1
                myChart.dispatchAction({
                    type: 'hideTip'
                })
                myChart.dispatchAction({
                    type:'downplay',
                })
            }
        });
        myChart.on('mouseover', (params) => {
            let dataIndex = params.dataIndex;
            let seriesIndex = params.seriesIndex;
            if(this.mapType == 'china'){
                if(params.componentType === "series" && params.componentSubType === "bar"){
                    clearInterval(that.chinaTimer)
                    that.chinaTimer = ''

                    myChart.dispatchAction({
                        type:'downplay',
                    })
                    myChart.dispatchAction({
                        type:'showTip',
                        seriesIndex: seriesIndex,
                        dataIndex:dataIndex
                    })
                    myChart.dispatchAction({
                        type:'highlight',
                        seriesIndex: seriesIndex + 1,
                        dataIndex:0
                    })
                    that.numbar = seriesIndex
                    that.numeffectScatter = seriesIndex + 1
                }else if(params.componentType === "series" && params.componentSubType === "effectScatter" && params.seriesName == "Overview"){
                    clearInterval(that.chinaTimer)
                    that.chinaTimer = ''
                    myChart.dispatchAction({
                        type:'downplay',
                    })
                    myChart.dispatchAction({
                        type:'showTip',
                        seriesIndex: seriesIndex - 1,
                        dataIndex:0
                    })
                    myChart.dispatchAction({
                        type:'highlight',
                        seriesIndex: seriesIndex,
                        dataIndex:dataIndex
                    })
                    that.numbar = seriesIndex - 1
                    that.numeffectScatter = seriesIndex
                }
            }else if(this.mapType == 'province'){
                if(that.effectdataIndex == dataIndex && that.effectseriesIndex == seriesIndex){
                    return false
                }
                if (params.componentType === "series" && params.componentSubType === "effectScatter" && params.seriesName != "Overview") {
                    myChart.dispatchAction({
                        type:'downplay',
                        seriesIndex: seriesIndex,
                        dataIndex:dataIndex
                    })
                }
            }
        });
        myChart.on('mouseout',(params) => {
            if(params.componentType === "geo" && !that.chinaTimer && that.mapType == "china"){
                that.Maptolltiptimer(myChart,myChart.getOption())
            }
            if(params.componentType === "geo" && !that.provinceTimer && that.mapType == "province"){
                that.Maptolltiptimer(myChart,myChart.getOption())
            }
        })
        myChart.on('legendselectchanged', (obj) => {
            that.effectdataIndex = -1
            that.effectseriesIndex = -1
            myChart.dispatchAction({
                    type:'downplay',
                })
            myChart.dispatchAction({
                type: 'hideTip'
            })
        });
        this.$refs.viewChina.addEventListener("click",() => {
            let option = JSON.parse(JSON.stringify(that.option))
            option.series = []
            let seriesArr = {
                name: 'Overview',
                type: 'scatter',
                coordinateSystem: 'geo',
                symbol: 'pin',
                symbolSize: [50,50],
                label: {
                    normal: {
                        show: true,
                        textStyle: {
                            color: '#fff',
                            fontSize: 9,
                        },
                        formatter (value){
                            return value.data.value[2]
                        }
                    }
                },
                tooltip:{
                    show:true,
                    backgroundColor:"transparent",
                    borderWidth:0,
                    padding:0,
                    extraCssText: 'box-shadow: 0 0 0px rgba(0, 0, 0, 0)',
                    position: function (pos, params, dom, rect, size) {
                        let x = pos[0]
                        let y = pos[1]
                        dom.style.transform = 'translateZ(0)'
                        return [rect.x+10,rect.y-100];
                    },
                    formatter:function(params){
                        let result = '';
                        return "<div>11111111</div>"
                    }
                },
                itemStyle: {
                    normal: {
                        color: '#2f94fa', //标志颜色
                    }
                },
                data: OverviewArr,
                showEffectOn: 'render',
                rippleEffect: {
                    brushType: 'stroke'
                },
                hoverAnimation: true,
                zlevel: 1
            }
            option.tooltip = {
                show:true,
                triggerOn: "none",
                backgroundColor:"transparent",
                borderWidth:0,
                padding:0,
                extraCssText: 'box-shadow: 0 0 0px rgba(0, 0, 0, 0)',
                position:(pos, params, dom, rect, size) => {
                    let x = pos[0]
                    let y = pos[1]
                    dom.style.transform = 'translateZ(0)'
                    return [rect.x+15,rect.y-5];
                },
                formatter:(params) => {
                    let result = `<div style="width: 120px;height: 32px;background: url(${Pic4}) center no-repeat;background-size: 100%;text-align:center;line-height:32px;color:#ffffff;font-size:14px">XXXX：${params.value / 100}</div>`
                    return result
                }
            }
            that.mapType = 'china'
            clearInterval(that.provinceTimer)
            that.provinceTimer = null
            myChart.setOption(option,true)
            // that.$store.commit('UpdatestationId', '');
            that.viewChina = false
            that.renderEachCity(myChart,OverviewArr)
        })
        this.renderEachCity(myChart,OverviewArr)
    },
    checkMap(name){
        switch (name) {
            case '新疆':
                return 'xinjiang'
                break;
            case '河北':
                return 'hebei'
                break;
            case '内蒙古':
                return 'neimenggu'
                break;
            case '黑龙江':
                return 'heilongjiang'
                break;
            case '甘肃':
                return 'gansu'
                break;
            case '青海':
                return 'qinghai'
                break;
            case '西藏':
                return 'xizhang'
                break;
            case '四川':
                return 'sichuan'
                break;
            case '云南':
                return 'yunnan'
                break;
            case '宁夏':
                return 'ningxia'
                break;
            case '山西':
                return 'shanxi'
                break;
            case '陕西':
                return 'shanxi3'
                break;
            case '北京':
                return 'beijing'
                break;
            case '山东':
                return 'shandong'
                break;
            case '河南':
                return 'henan'
                break;
            case '安徽':
                return 'anhui'
                break;
            case '江苏':
                return 'jiangsu'
                break;
            case '浙江':
                return 'zhejiang'
                break;
            case '福建':
                return 'fujian'
                break;
            case '广东':
                return 'guangdong'
                break;
            case '台湾':
                return 'taiwan'
                break;
            case '湖南':
                return 'hunan'
                break;
            case '湖北':
                return 'hubei'
                break;
            case '江西':
                return 'jiangxi'
                break;
            case '重庆':
                return 'chongqing'
                break;
            case '广西':
                return 'gaungxi'
                break;
            case '贵州':
                return 'guizhou'
                break;
            case '海南':
                return 'hainan'
                break;
            case '吉林':
                return 'jilin'
                break;
            case '辽宁':
                return 'liaoning'
                break;
            default:
                break;
        }
    },
    renderEachCity(myChart,OverviewArr) {
        let rawData = OverviewArr;
        console.log(OverviewArr)
        let max,maxArr = []
        OverviewArr.forEach((item,index) => {
            maxArr.push(item.value[2])
        })
        max = Math.max(...maxArr)
        let option = {
            xAxis: [],
            yAxis: [],
            grid: [],
            series: []
        };
        let dom = 200;
        let barWidth = dom / 20;
        echarts.util.each(rawData, function(dataItem, idx) {
            let coord = myChart.convertToPixel('geo', dataItem.value);
            idx += '';
            option.xAxis.push({
                id: idx,
                gridId: idx,
                type: 'category',
                name: '', //dataItem[0] 柱状体底部名称
                nameLocation: 'middle',
                nameGap: 3,
                splitLine: {
                    show: false
                },
                axisTick: {
                    show: false
                },
                axisLabel: {
                    show: false
                },
                axisLine: {
                    show: false,
                    onZero: false,
                    lineStyle: {
                        color: '#666'
                    }
                },
                // data: xAxisCategory,
                data: [dataItem.name],
                z: 5

            });
            option.yAxis.push({
                id: idx,
                gridId: idx,
                // type: "log",
                // interval:10* 100, //每次增加几个
                max:max * 100,
                splitLine: {
                    show: false
                },
                axisTick: {
                    show: false
                },
                axisLabel: {
                    show: false
                },
                axisLine: {
                    show: false,
                    lineStyle: {
                        color: '#1C70B6'
                    }
                },
                z: 5
            });
            option.grid.push({
                id: idx,
                width: 80,
                height: 80,
                left: coord[0] - 40,
                top: coord[1] - 75,
                z: 100,
                show:false,
            });
            option.series.push(
                {
                    type: 'bar',
                    barWidth: barWidth,
                    id: idx,
                    xAxisId: idx,
                    yAxisId: idx,
                    z: 20000,
                    itemStyle: {
                        normal: {
                            barBorderRadius: 28,
                            color: new echarts.graphic.LinearGradient(0, 0, 0, 1,//4个参数用于配置渐变色的起止位置, 这4个参数依次对应右/下/左/上四个方位. 而0 0 0 1则代表渐变色从正上方开始
                                [
                                    {offset: 0, color: '#01fbff'},
                                    {offset: 0.1, color: '#48e1fc'},
                                    {offset: 1, color: '#0248ba'}
                                ]                //数组, 用于配置颜色的渐变过程. 每一项为一个对象, 包含offset和color两个参数. offset的范围是0 ~ 1, 用于表示位置
                            )
                        }
                    },
                    label: {
                        show: false,
                        position: [barWidth / 2, -(barWidth + 20)],
                        color: '#ffffff',
                        fontSize: 12,
                        fontStyle: 'bold',
                        align: 'center',
                    },
                    data: [dataItem.value[2] * 100]
                },
                {
                    name: 'Overview',
                    type: 'effectScatter',
                    coordinateSystem: 'geo',
                    rippleEffect: {
                        brushType: "fill",
                        scale: 2.5,
                    },
                    tooltip:{
                        show:false,
                    },
                    geoIndex:0,
                    // xAxisIndex:idx,
                    // yAxisIndex:idx,
                    showEffectOn: "emphasis",
                    itemStyle: {
                        normal: {
                            color: 'rgba(17,251,255,0.4)',
                            borderWidth:1,
                            borderColor:'rgba(17,251,255,1)',
                            opacity:1
                        }
                    },
                    data: [
                        {name:dataItem.name,value:dataItem.value},
                    ],
                    legendHoverLink: false,
                    z:150,
                    symbolSize: 30,
                },
                {
                    name:'a',
                    tooltip:{
                    show:false 
                    },
                    type: 'pictorialBar',
                    xAxisId: idx,
                    yAxisId: idx,
                    itemStyle: {
                        normal: {
                            color: new echarts.graphic.LinearGradient(
                                0, 0, 1, 0,
                                [
                                    {offset: 0, color: '#00fbff'},
                                    {offset: 1, color: '#00fbff'}
                                ]
                            ), 
                            borderWidth:1,
                            borderColor:'#00fbff'
                        }
                    },
                    symbol: 'circle',
                    symbolSize: barWidth,
                    symbolPosition: 'end',
                    data: [dataItem.value[2] * 100],
                    z:999999999
                },
            );
        });
        myChart.setOption(option);
        this.Maptolltiptimer(myChart,option)
    },
    Maptolltiptimer(myChart,option){
        let that = this;
        if(this.mapType == 'china'){
            this.chinaTimer = setInterval(() => {
                myChart.dispatchAction({
                        type:'downplay',
                    })
                myChart.dispatchAction({
                    type: 'hideTip'
                })
                myChart.dispatchAction({
                    type:'showTip',
                    seriesIndex: that.numbar,
                    dataIndex:0
                })
                myChart.dispatchAction({
                    type:'highlight',
                    seriesIndex: that.numeffectScatter,
                    dataIndex:0
                })
                if(that.numeffectScatter == option.series.length - 2){
                    that.numbar = 0
                    that.numeffectScatter = 1
                }else{
                    that.numbar += 3
                    that.numeffectScatter += 3
                }
            }, 5000);
        }else if(this.mapType == 'province'){
            this.provinceTimer = setInterval(() => {
                if(option.series.length > that.provinceseriesIndex + 1){
                    if(option.series[that.provinceseriesIndex].data.length > that.provincedataIndex + 1){
                        that.provincedataIndex++
                    }else{
                        that.provinceseriesIndex++
                        that.provincedataIndex = 0
                    }
                }else{
                    that.provinceseriesIndex = 0
                    that.provincedataIndex = 0
                }
                that.effectseriesIndex = that.provinceseriesIndex
                that.effectdataIndex = that.provincedataIndex
                myChart.dispatchAction({
                    type:'downplay',
                })
                myChart.dispatchAction({
                    type: 'hideTip'
                })
                myChart.dispatchAction({
                    type:'showTip',
                    seriesIndex: that.provinceseriesIndex,
                    dataIndex:that.provincedataIndex
                })
                myChart.dispatchAction({
                    type:'highlight',
                    seriesIndex: that.provinceseriesIndex,
                    dataIndex:that.provincedataIndex
                })
            },5000)
        }
    },
  },
  destroyed(){
      clearInterval(this.chinaTimer)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.wrap-map{
    position: relative;
    width: 51%;
    height:830px;
}
.echarts-map{
    width:100%;
    height:830px;
    background: url(../../static/daping/img/bg-04.png) top left no-repeat;
    background-size: 100%;
    position: absolute;
    left: 0;
    top: 0;
}
.rhoaias{
    width:100%;
    height:830px;
    position: absolute;
    left: 0;
    top: 0;
}
.rhoaias-one{
    width: 690px;
    height: 690px;
    background: url(../../static/daping/img/pic-18.png) center no-repeat;
    background-size: 100%;
    position: absolute;
    left: 150px;
    animation:circle 30s infinite linear; 
}
.rhoaias-two{
    width: 602px;
    height: 576px;
    background: url(../../static/daping/img/pic-19.png) center no-repeat;
    background-size: 100%;
    position: absolute;
    left: 195px;
    top: 55px;
    animation:backcircle 25s infinite linear; 
}
.rhoaias-three{
    width: 530px;
    height: 531px;
    background: url(../../static/daping/img/pic-20.png) center no-repeat;
    background-size: 100%;
    position: absolute;
    left: 229px;
    top: 77px;
    animation:circle 40s infinite linear; 
}
@keyframes circle{
    0% {transform:rotate(0deg);}
    100% {transform:rotate(-360deg);}
}
@keyframes backcircle{
    0% {transform:rotate(-360deg);}
    100% {transform:rotate(0deg);}
}
.map-nav{
    position: absolute;
    z-index: 9999;
    width: 300px;
    height: 75px;
    left: 33%;
    top: 0;
    background: url(../../static/daping/img/btn-02.png) center no-repeat;
    text-align: center;
}
.map-nav span{
    font-size: 16px;
    color: #ffffff;
    display: inline-block;
    padding-top: 36px;
    text-align: center;
}
.overviewdata{
    width: 168px;
    height: 78px;
    background:url(../../static/daping/img/pic-05.png) center no-repeat;
    background-size: 100%;
    position: absolute;
    z-index: 9999;
    left: 5%;
    top: 1%;
    cursor: pointer;
}
</style>

