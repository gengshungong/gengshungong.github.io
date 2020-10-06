---
layout: post
title: 'Antd 穿梭框 自定义处理'
date: 2019-09-15
categories:
  - antd
tag:
  - antd
---

<p>1.首先引入antd组件</p>
```
 import {
Checkbox,
Transfer,
Input,	
} from ‘antd’
const { Search } = Input

```

<p>2.然后进行自定义穿梭框和相应的函数方法</p>

```

const isChecked = (selectedKeys: any, eventKey: any) => {
  return selectedKeys.indexOf(eventKey) !== -1;
};

const isDisabled = (checkedKeys: any, eventKey: any) => {
  return checkedKeys.includes(eventKey)
}
//  自定义穿梭框
const TreeTransfer = (data: any) => {
  const { dataSource, targetKeys, onSearch, ...restProps } = data
  const transferDataSource: any[] = [];
  function flatten(list: any[]) {
    list.forEach(item => {
      transferDataSource.push(item);
    });
  }
  flatten(dataSource);
  return (
    <Transfer
      {...restProps}
      targetKeys={targetKeys}
      dataSource={transferDataSource}
      className="tree-transfer"
      render={item => item.title}
      listStyle={{
        width: 250,
        height: 300,
        overflow: 'auto'
      }}
    >
      {(props: any) => {
        const { direction, selectedKeys, onItemSelect, onItemSelectAll } = props
        if (direction === 'left') {
          const checkedKeys = [...selectedKeys, ...targetKeys];
          return (
            <div>
              <Search
                placeholder="请输入管理单位"
                onSearch={onSearch}
                style={{ width: 180 }}
              />
              {
                <Checkbox.Group onChange={(value: any) => {
                  onItemSelect(value, !isChecked(checkedKeys, value))
                  onItemSelectAll(value, !isChecked(checkedKeys, value))
                }
                } value={checkedKeys} defaultValue={targetKeys}>
                  {
                    dataSource.map((item: any) => (
                      <div className="checkbox">
                        <Checkbox value={item.key} disabled={isDisabled(targetKeys, item.key)}>
                          {item.title}
                        </Checkbox>
                      </div>
                    ))
                  }
                </Checkbox.Group >
              }
            </div>)
        } else {
          return false
        }
      }
      }
    </Transfer>)
}

```


<p>2.最后进行自定义穿梭框的引入</p>

```

this.state = {
      mockData: [],
      newtargetKeys: []
    };

public newhandleChange = (targetKeys: any) => {
    this.setState({ newtargetKeys: targetKeys });
  };
public handleSearch = (dir: any, value:any) => {
console.log(‘dir’,dir,’value’,value)
}

<TreeTransfer
            dataSource={this.state.mockData}
            targetKeys={this.state.newtargetKeys} //这个可以自己定义
            onChange={this.newhandleChange} //方法可以自己定义
            onSearch={this.handleSearch}
          />

```

```
