---
title: react onClick 事件
date: 2018-06-12 23:22:28
tags: react
---


1. jsx 里面,onClick={this.函数名}来绑定事件
2. this引用的问题，需要在构造函数里面用bind绑定this
3. this.setState修改state,是返回新的state，而不是修改


### this的用法如下
- 方法一

```
class First extends React.Component {
    constructor(props){
        super(props)
        this.state={
            arr: [ 'AAA', 'BBBB', 'CCCC' ]
        }
        this.add = this.add.bind(this); // 绑定this的方法
    }
    add(){
        console.info('测试onclick的事件');
        this.setState({
            arr:[...this.state.arr,'DDDD '+Math.random()]
        })
    }

    render(){
        return(
            <div>
                <button onClick={this.add}>点击添加数据</button>
                <ul>
                    { this.state.arr.map(v=>{
                        return <li key={v}>{v}</li>
                    })}
                </ul>
            </div>
        )
    }
}
```
> 强制在constructor里面的通过bind来绑定this，但是函数一旦多起来，就比较繁琐

- 方法二

```
class First extends React.Component {
    constructor(props){
        super(props)
        this.state={
            arr: [ 'AAA', 'BBBB', 'CCCC' ]
        }
    }
    add(){
        console.info('测试onclick的事件');
        this.setState({
            arr:[...this.state.arr,'DDDD '+Math.random()]
        })
    }

    render(){
        return(
            <div>
                <button onClick={()=>this.add()}>点击添加数据</button>
                <ul>
                    { this.state.arr.map(v=>{
                        return <li key={v}>{v}</li>
                    })}
                </ul>
            </div>
        )
    }
}
```
> 当前触发函数位置使用尖头函数，非常方便 ，另外一种等价的方法也是尖头函数的方法如下

```
    add = () => {
        console.info('测试onclick的事件');
        this.setState({
            arr:[...this.state.arr,'DDDD '+Math.random()]
        })
    }
```
