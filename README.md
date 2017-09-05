# echarts
echarts练习


# echarts配置

## 全局
```
遇到的问题: 
  tab选项卡,多个页面有echarts图表时,canvas图表的宽高如果设置的百分比,
  当display:none-->转为display:block时,
  图表是没有宽高的,默认为100px
  解决办法:
  当mychart.resize时,设置width为直接父元素的宽高
window.onresize = function () {
    myYSChart.resize(); //使第一个图表适应
}
```

##title
```
title: {
    subtext : '数量/日期',
    left: '2%',
    bottom: '10%',
    // subtextStyle: { 标题样式
    //     color: 'red'
    // }
}
```

## yAxis
```
yAxis: {
    show: true, // 显示坐标轴
    splitLine:{ //去除网格线
        show: false
    },
    splitArea : {//保留网格区域
        show : true
    },
    axisLine: { //隐藏Y轴线
        show: false,
        lineStyle:{ //坐标轴文字样式
            color: '#8b8b8b'
        }
    },
    axisTick : { //显示刻度线
        show: false
    }, 
    axisLabel: {
        interval: 0, // 隔0天显示一个刻度
        textStyle: {
            color: '#fff'
        }
    },
    gridLineWidth: 0, //网格线宽度
    lineColor: "#8b8b8b", //轴线颜色
    tickColor: "#8b8b8b", // 刻度线颜色
    gridLineColor: "#f0f0f0", //网格线颜色
    categories:data[0],
    tickInterval: Math.ceil(data[0].length / 7), // 刻度值
}
```
## series // 数据
```
barMaxWidth:30,//柱子最大宽度
label: {
        position: 'top', //数据显示在柱图顶部 如果不设置: 鼠标移入的时候,数据会隐藏
        textStyle: {
            // 柱图上面数据文本样式
        },
        formatter: function(params) { // 只显示数据中的指定数据在柱形图顶部
            return params.data
        }
    }
},
itemStyle: { // 数据样式
    normal: {
        color: function(params) {
            var colorList = [
              '#c43343','#0dff90'
            ];
            if(params.data < 0) { // 如果数据 < 0, 设置不同颜色
                return colorList[1];
            }
            return colorList[0];
        },
        label: {
            show: true,
            position: 'top',
            formatter: '{b}\n{c}'
        }
    }
}
```

## tooltip // 图例
```
tooltip : {
    trigger: 'axis', // 指定触发的项目---x轴
    axisPointer : {            // 坐标轴指示器，坐标轴触发有效
        type : 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
    },
    textStyle: { // 图例字体样式
        fontSize: 12
    },
    backgroundColor: 'rgba(0,0,0)',   // 背景颜色
    borderColor: '#3b9ce0',       // 边框颜色
    formatter: function (params) { // 提示框格式化字符串 鼠标悬浮在柱子上显示的提示文本
        var tar = params[0]; // 显示单量,盈亏点数,时间
        return '盈利总盈点: '+tar.data+''+'<br/>'+'盈亏总盈点比例: '+dataYS[1][tar.dataIndex]+'%';
    }
}
```

##legend
```
legend: { 
    right: 20, // 位置
    data: [{
        name: '1',
        // 强制设置图形为长方形。
        icon: 'rect',
        // 设置文本为白色
        textStyle: {
            color: '#fff'
        }
    }]
},
```

```
