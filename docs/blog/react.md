# React 浅析

## React 生命周期

### 创建时

#### constructor

React 组件的构造函数将会在装配之前被调用。

构造函数是初始化状态的合适位置，可以基于属性来初始化状态。

#### static getDerivedStateFromProps

组件实例化后和接受新属性时将会调用 getDerivedStateFromProps。它应该返回一个对象来更新状态，或者返回 null 来表明新属性不需要更新任何状态。

getDerivedStateFromProps 只存在一个目的。它使组件能够根据 props 的更改来更新其内部状态。

#### render

将虚拟 DOM 渲染成真实的 DOM。

#### componentDidMount

在组件被装配后立即调用。初始化使得 DOM 节点应该进行到这里。`若你需要从远端加载数据，这是一个适合实现网络请求的地方。`在该方法里设置状态将会触发重渲。

您可以调用 setState()立即在 componentDidMount()。它将触发额外的渲染，但它将在浏览器更新屏幕之前发生。这保证即使 render()在这种情况下将被调用两次，用户也不会看到中间状态。

### 更新时

#### getDerivedStateFromProps

同上。

#### shouldComponentUpdate

此方法仅作为性能优化存在。不要依赖它来“防止”渲染，因为这可能导致错误。考虑使用内置 PureComponent 而不是 shouldComponentUpdate()手写。

#### render

将虚拟 DOM 渲染成真实的 DOM。

#### getSnapshotBeforeUpdate

- 触发时间: update 发生的时候，在 render 之后，在组件 dom 渲染之前。
- 返回一个值，作为 componentDidUpdate 的第三个参数。

#### componentDidUpdate

componentDidUpdate(prevProps, prevState, snapshot)

将此作为在更新组件时对DOM进行操作的机会。只要您将当前道具与之前的道具进行比较（例如，如果道具未更改，则可能不需要网络请求），`这也是进行网络请求的好地方。`

### 卸载时

#### componentWillUnmount

componentWillUnmount()在卸载和销毁组件之前立即调用。在此方法中执行任何必要的清理，例如使计时器无效，取消网络请求或清除在其中创建的任何订阅。

### 弃用生命周期

#### componentWillMount

componentWillMount是在render之前执行，所以在这个方法中setState不会发生重新渲染(re-render)。

通常情况下，推荐用constructor()方法代替。

#### componentWillReceiveProps

UNSAFE_componentWillReceiveProps(nextProps)

使用不当可能体现为组件陷入渲染死循环，他会一直接受新的外部状态导致自身一直在重渲染。

[生命周期图](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)
