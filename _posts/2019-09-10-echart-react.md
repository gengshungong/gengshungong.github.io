---
layout: post
title:  "echarts 相关的属性和用法"
date:   2019-09-10
categories: "echarts"
tag:
- echarts
--- 

## 柱状图
```
    public getOption = () => {
        return {
            // 标题
            title: {
                text: '任务量',
                left: 20,
                textStyle: {
                    color: '#fff',
                    fontSize: 14,
                }
            },
            color: '#2979FF',
            // 浮框
            tooltip: {
                trigger: 'axis',
                axisPointer: {            // 坐标轴指示器，坐标轴触发有效
                    type: 'shadow'        // 默认为直线，可选为：'line' | 'shadow'
                }
            },
            grid: {
                left: '5%',
                right: '1%',
                bottom: '10%',
                top: '14%',
                containLabel: false
            },
            dataZoom: [{
                type: 'inside',
                show: true,
                start: 0,
                end: 60,
            }
            ],
            xAxis: [
                {
                    type: 'category',
		  boundaryGap: false  //刻度从0开始 true 是不从0开始
                    max: 20,
                    data: this.optionData && this.optionData.map((option: any) => (
                        {
                            value: option.name,
                            textStyle: {
                                color: 'rgba(255, 255, 255, 0.5)'
                            }
                        }
                    )),
                    axisTick: {
                        show: false,
                        alignWithLabel: false
                    },
                    axisLine: {
                        lineStyle: {
                            color: 'rgba(41, 121, 255, 0.2)'
                        },
                    },
                    boundaryGap: ['5%', 0]
                }
            ],
            yAxis: [
                {
                    type: 'value',
			max:2000，
	splitNumber : 5,   //把y轴分为5段,一般和max，min配合使用
                    axisLine: {
                        show: false,
                        lineStyle: {
                            color: 'rgba(255, 255, 255, 0.5)'
                        }
                    },
                    // 背景线
                    splitLine: {
                        lineStyle: {
                            color: 'rgba(41, 121, 255, 0.2)'
                        }
                    },
                    axisTick: {
                        show: false,
                    },
                }
            ],
            series: [
                {
                    type: 'bar',
                    barWidth: '50%',
                    data: this.optionData && this.optionData.map((option: any) => option.count),
itemStyle: {
        normal: {
            color: new echarts.graphic.LinearGradient(
                0, 0, 0, 1,       //4个参数用于配置渐变色的起止位置, 这4个参数依次对应右/下/左/上四个方位. 而0 0 0 1则代表渐变色从正上方开始
                [
                    {offset: 0, color: '#000'},
                    {offset: 0.5, color: '#888'},
                    {offset: 1, color: '#ddd'}
                ]                //数组, 用于配置颜色的渐变过程. 每一项为一个对象, 包含offset和color两个参数. offset的范围是0 ~ 1, 用于表示位置
            )
        }
    }        //颜色渐变

                }
            ]
        }
    }

```

## 饼图

``` 
  public bigtaskOption = () => {
        return {
            tooltip: {
                formatter: '{b}'
            },
            graphic: {
                type: 'text',
                left: 'center',
                top: 'center',
                style: {
                   text: `任务总数\n\r${this.bigtask && this.bigtask}`,
                    fontSize: 14,
                    textAlign: 'center',
                    fill: '#00DAD8'
                }
            },
            labelLine: {
                lineStyle: {
                    color: '#00DAD8',
                }
            },
            series: [
                {
                    name: '任务总数',
                    type: 'pie',
                    roseType: 'area',
                    radius: [40, 100],
                    center: ['50%', '50%'],
                    label: {
                        normal: {
                            textStyle: {
                                color: '#fff'
                            }
                        }
                    },
                    data: this.tasktypeData.statistics && this.tasktypeData.statistics.map((item: any) => (
                        { value: item.ratio, name: `${item.name}\n\r${Number(item.ratio * 100).toFixed(2)}%` }
                    )),
                }
            ]
        }
    }
```

