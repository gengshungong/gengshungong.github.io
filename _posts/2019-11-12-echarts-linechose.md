---
layout: post
title:  "echarts 自定义处理"
date:   2019-11-12
categories: 
- echarts
tag:
- echarts 
--- 

##### 1.首先自定义页面dom结构
```js
var html = `<div class="select dowebok" id="two">
    <span class="placeholder">请选择</span>
    <ul class="area-list">
    </ul>
</div>`
```
##### 2.自定义编写echarts组件

```js
function echartsCode() {

    // 自定义areaStyle
  var areaStyle = [
    {
      color: {
        type: 'linear',
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [{ offset: 0, color: 'rgba(255,105,61,100)' },
        { offset: 1, color: 'rgba(255,105,61,0)' }]
      },
      opacity: 0.1
    },
    {
      color: {
        type: 'linear',
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [{ offset: 0, color: 'rgba(230,149,43,100)' }, { offset: 1, color: 'rgba(230,149,43,100)' }]
      },
      opacity: 0.1
    },
    {
      color: {
        type: 'linear',
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [{ offset: 0, color: 'rgba(83,204,250,100)' }, { offset: 1, color: 'rgba(83,204,250,0)' }]
      },
      opacity: 0.1
    },
  ],


  // 定义option
  option = {
    tooltip: {
      trigger: 'axis'
    },
    color: ['rgba(255,105,61,96)', 'rgba(230,149,43,100)', 'rgba(83,204,250,100)'],
    legend: {
      data: [],
      //selectedMode: 'single',
      type: 'scroll',
      left: '150px',
      top: '8px',
      textStyle: {
        color: '#fff'
      }
    },
    grid: {
      left: '3%',
      right: '4%',
      bottom: '0%',
      containLabel: true
    },

    xAxis: {
      type: 'category',
      boundaryGap: false,
      axisLabel: {
        color: '#fff'
      },
      data: chart.views[2].data.x[0].data,
      splitLine: {
        lineStyle: {
          color: '#ccc',
        }
      }
    },
    yAxis: {
      type: 'value',
      axisLabel: {
        color: '#fff'
      },
      splitLine: {
        lineStyle: {
          color: '#ccc',
          opacity: 0.1
        }
      }
    },
    series: []
  };
  var _yData = chart.views[0].data.y
  var _yData1 = chart.views[1].data.y
  var listHtml = ''
  var tempArr = []
  var liIndex = -1
  for (var i of _yData) {
    if (!tempArr.includes(i.compare_names[1])) {
      liIndex++
      tempArr.push(i.compare_names[1])
      listHtml += `<li data-index = '${liIndex}'>${i.compare_names[1]}</li>`
    }
  }
  $('.area-list').html(listHtml)


// 相关自定义操作
  $('.select').on('click', '.placeholder', function (e) {
    var parent = $(this).closest('.select');
    if (!parent.hasClass('is-open')) {
      parent.addClass('is-open');
      $('.select.is-open').not(parent).removeClass('is-open');
    } else {
      parent.removeClass('is-open');
    }
    e.stopPropagation();
  }).on('click', 'ul>li', function () {
    //console.log(_yData1[0].data[this.getAttribute('data-index')])
    option.series = []
    option.legend.data = []
    var parent = $(this).closest('.select');
    parent.removeClass('is-open').find('.placeholder').text($(this).text());
    var x = -1;
    var index = $(this).text() === '内部核心圈' ? 0 : 1


// 自定义series
    option.series.push({
      name: _yData[index].compare_names[2],
      type: 'line', markLine: {
        silent: true,
        label: {
          position: 'middle'
        },
        markPoint: {
          data: [
            {
              type: 'max'
            }
          ]
        },
        data: [
          {
            yAxis: _yData1[0].data[parseInt(this.getAttribute('data-index'))],//黄色警告值,注意下面还有个黄色值需要改
            lineStyle: {
              color: "#e6a953"
            }
          },
          {
            yAxis: _yData1[1].data[parseInt(this.getAttribute('data-index'))],//红色报警值，注意下面还有个红色值需要改
            lineStyle: {
              color: "red"
            }
          }
        ]
      },
      symbol: 'none',
      lineStyle: {
        //color:'#4eb9ff',
        width: 2
      },
      smooth: true,
      data: _yData[index].data,
      areaStyle: areaStyle[index % 3]
    })
    option.legend.data.push({
      name: _yData[index].compare_names[2],
      icon: 'line',
    })
    option.series.push({
      name: '预测值',
      type: 'line',
      data: _yData2[index].data,
      markLine: {
        silent: true,
        label: {
          position: 'middle'
        },
        data: [
          {
            yAxis: _yData1[index],//黄色警告值
            lineStyle: {
              color: "#e6a953"
            }
          },
          {
            yAxis: _yData1[index],//红色报警值
            lineStyle: {
              color: "#f65f2c"
            }
          }
        ]
      },
      markPoint: {
        data: [
          {
            type: 'max',

          },
        ],
        itemStyle: {
          color: 'gray'
        }
      },
      areaStyle:
      {
        color: {
          type: 'linear',
          x: 0,
          y: 0,
          x2: 0,
          y2: 1,
          colorStops: [{ offset: 0, color: 'gray' }, { offset: 1, color: '#fff' }]
        },
        opacity: 0.1
      },
      symbol: 'none',
      lineStyle: {
        color: 'gray',
        width: 1,
        type: "dotted"
      },
      smooth: true,
    })
    myChart.setOption(option);
  });

  $('body').on('click', function () {
    $('.select.is-open').removeClass('is-open');
  });
  $('.placeholder').text(_yData[0].compare_names[1])
  var _y = -1
  for (let i of _yData) {
    _y++
    if (i.compare_names[1] == _yData[0].compare_names[1]) {
      option.series.push({
        name: i.compare_names[2],
        type: 'line',
        data: i.data,
        symbol: 'none',
        smooth: true,
        lineStyle: {
          //color:'#4eb9ff',
          width: 2
        },
        markLine: {
          silent: true,
          label: {
            position: 'middle'
          },
          data: [
            {
              yAxis: _yData1[0].data[0],//黄色警告值
              lineStyle: {
                color: "#e6a953"
              }
            },
            {
              yAxis: _yData1[1].data[0],//红色报警值
              lineStyle: {
                color: "#f65f2c"
              }
            }
          ]
        },
        markPoint: {
          data: [
            {
              type: 'max'
            }
          ]
        },
        areaStyle: areaStyle[_y % 3]
      })
      option.legend.data.push({
        name: i.compare_names[2],
        icon: 'line'
      })
    }
  }


// 第二部分
  var _y = -1
  var _yData2 = chart.views[2].data.y
  option.series.push({}
    name: '预测值',
    type: 'line',
    data: _yData2[0].data,
    markLine: {
      silent: true,
      label: {
        position: 'middle'
      },
      data: [
        {
          yAxis: _yData1[0],//黄色警告值
          lineStyle: {
            color: "#e6a953"
          }
        },
        {
          yAxis: _yData1[0],//红色报警值
          lineStyle: {
            color: "#f65f2c"
          }
        }
      ]
    },
    markPoint: {
      data: [
        {
          type: 'max',

        },

      ],
      itemStyle: {
        color: 'gray'
      }
    },
    areaStyle:
    {
      color: {
        type: 'linear',
        x: 0,
        y: 0,
        x2: 0,
        y2: 1,
        colorStops: [{ offset: 0, color: 'gray' }, { offset: 1, color: '#fff' }]
      },
      opacity: 0.1
    },

    symbol: 'none',

    lineStyle: {
      color: 'gray',
      width: 1,
      type: "dotted"
    },
    smooth: true,
  })

  // 自定义legend
  option.legend.data.push({
    name: i.nick_name,
    icon: 'line'
  })
  // 粘贴代码结束
  return option
}
```

#### `此代码仅供借鉴学习`