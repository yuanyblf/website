+++
title = "React"
date = "2017-02-01"
draft = false
weight= 2
+++

# React

- 本项目使用React与Mobx作为前端框架，React 的核心思想是：封装组件。各个组件维护自己的状态和 UI，当状态变更，自动重新渲染整个组件。我们不再需要查找某个 DOM 元素，然后操作 DOM 去更改 Mobx 是 JavaScript 状态容器，提供可预测化的状态管理。

```
import React, { Component, PropTypes } from 'react';
import { observer, injext } from 'mobx-react';

@inject('AppState')
@observer
class Dashboard extends Component {
  constructor(props) {
    super(props);
  };
  componentDidMount(){};
  static propTypes = {
  };
  static contextTypes = {
    router: PropTypes.object.isRequired
  };
  render() {
    return (
      <div style={{ backGroundColor: "red", width: "100px", height: "100px"}}>
      </div>
    )
  }
}
function mapStateProps(state) {
  return {
  };
}
module.exports = Dashboard;
```

- [React](#react)