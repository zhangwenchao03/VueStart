# vuestart

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
[2018 前端性能优化清单](https://juejin.im/post/5a966bd16fb9a0635172a50a)
[HTTP缓存机制详解](https://juejin.im/entry/599afbe5f265da247c4ee6e3)
[算法刷题](https://leetcode-cn.com/explore/interview/card/top-interview-questions-easy/6/linked-list/44/)
[深入理解react中的虚拟DOM、diff算法](https://www.cnblogs.com/zhuzhenwei918/p/7271305.html)
[页面生命周期——DOMContentLoaded&Loaded](https://juejin.im/post/59e49851f265da430b7a4bb8)
[页面重绘和回流以及优化](https://www.html.cn/archives/4996)
[JavaScript 内存机制（前端同学进阶必备)](https://juejin.im/post/5b10ba336fb9a01e66164346)
[https://juejin.im/post/5a96230af265da4e865a9f65](https://juejin.im/post/5a96230af265da4e865a9f65)
[其它学习资料](https://blog.fundebug.com/)
[其它面试资料](https://yuchengkai.cn/docs/frontend/#typeof)

1.当state或者props改变的时候render就会执行，父组件的render执行的时候子组件的render就会执行
  setState()是第一个参数是异步函数，第二个参数是回调函数
2.虚拟Dom更新界面 
  1.state数据 
  2.JSX模板 
  3.数据+模板结合生成虚拟DOM（虚拟DOM是一个js对象，用来描述真实DOM） 用虚拟DOM生成真实DOM
  4.当state发生变化时 数据和模板生成新的虚拟DOM，比较两个虚拟DOM的区别（同层比对 ），然后更新真实DOM
  优点：1.性能提升2.跨端应用 react native
3.生命周期函数:某一时刻会被自动执行的函数 render也是
  mount: componentWillMount->render -> componentDidMount
  update: props：componentWillReciveProps -> shouldComponentUpdate (返回true)-> componentWillUpdate -> render -> componentDidUpdate  
				 componentWillReciveProps：组件从父组件接受参数，且组件不是第一次存在于父组件中，才会执行
		  state: shouldComponentUpdate (返回true)-> componentWillUpdate -> render -> componentDidUpdate
  unmounting: componentWillUnmount
4.store必须是唯一的 只有store能改变自己的state，reducer 不能修改state 而且reducer必须是纯函数（固定的输入返回固定的输出 且不会有副作用）
  createStore创建store store.dispatch分发action store.getState获取所有state数据 store.subscribe监控store数据变动
5.组件拆分成UI组件和容器组件 UI组件负责组件的渲染 容器组件负责组件的逻辑
6.一个文件引入css文件，css全局生效
7.memo()包括函数组件属性不变时不重复渲染 useEffect渲染结束执行 useMemo渲染时执行，所以不要有副作用 如果useMemo的返回值是函数，就可以写成useCallback，
  useCallback解决传入子组件的函数变化，导致子组件过度渲染问题
  memo 实例: const Foo = memo(function Foo(props) {
    return ()
  })
  例如父组件中: 如果直接传click的函数，则每次父组件重新渲染时 onClick函数都会重新创建，函数句柄都会发生变化，导致传给子组件后子组件重新渲染
  const onClick = useCallBack(()=>{console.log('click')},[])
  return (
	<Count onClick={onClick}/>
  )
  useMemo和useCallBack依赖变化时肯定会重新执行，依赖不变时不一定不会重新执行，所以只能当做锦上添花的优化手段
  
8.useRef() 
  你不能在函数组件上使用 ref 属性，因为它们没有实例，可以在函数组件内部使用 ref 属性，只要它指向一个 DOM 元素或 class 组件，指向class组件时（<Count    	ref={ref1}/>）经常被用来调用函数组件的方法，也可以把useRef的current指定某个值也可以把useRef的current指定某个值,例如在组件中声明一个ref const timer = useRef();
  然后如果存在一个副作用中起一个定时器 timer.current = setTimeout(),在另一个副作用中清除定时器时可以用clearTimeout(timer.current),如果不用useRef绑定变量
  的句柄 就清不掉
9.只能在函数组件或者自定义hooks函数里面调用hooks
10.hooks优势 1.副作用的关注点分离 2.函数组件没有class组件this指针的问题 3.方便复用状态逻辑（自定义hook）自定义hook也可以像函数组件一样返回jsx模板，返回值也是
自定义的，所以函数组件和自定义hooks很像，只有输入输出的区别
11.类组件部分生命周期函数映射到函数组件
function App() {
 useEffect(()=>{
      //componentDidMount 第一次渲染结束调用
	  return ()=>{
		//componentWillUnmount 最后一次渲染结束之前
	  }
 },[])
 let renderCounter = useRef(0);
 renderCounter.current ++
 useEffect(() => {
	if (renderCounter.current > 1) {
	  //componentDidUpdate 不是第一次渲染 相当于componentDidUpate
	}
 })
}
10 ,首次加载性能问题 lazy Suspense实现延迟加载，Suspense 接受一个fallback属性 属性值是jsx 表示异步加载之前显示什么
   const Example = lazy(() => import('./Example.js')
   。。。
   return (
	<div>
		<Suspense fallback = {<div>loading</div>}
		  <Example/>
		</Suspense>
	</div>
   )
11.发布npm包 调试： 例如newoidc包源码 yarn link, 然后工程add newoidc后，yarn link “newoidc”，这样源码build以后工程能随时联动调试
12.git
git reset --hard 强制覆盖本地
 在分支git pull origin获取最新代码 、ls:文件夹 、git checkout -b feature/zhagnwenchao ；创建本地分支并切到分支、、切到当前分支后 git merge dev：合并dev分支到当前分支、
切到dev后git pull origin dev 获取dev分支最新代码、git push origin feature/zhagnwenchao：创建远程分支并将本地分支提交
stash 保存当前修改 pop stash 恢复当前修改


$ git reset --hard origin/master 与master分支保持一致

hotfix 往dev 的pr 冲突  本地分支 merge dev  然后merge hotfix  解决冲突  本地推到dev

git remote update origin --prune   # 更新远程主机origin 整理分支


## 习惯
[8 个 Tips 让你更好的进行 Code Review](https://blog.fundebug.com/2019/05/16/8-tips-for-great-code-reviews/)
[如何写出少bug的代码，你需要这4点建议](https://blog.fundebug.com/2018/08/09/four-clean-code-tips/)
[写给工程师的十条精进原则](https://blog.fundebug.com/2018/09/13/10-principle-for-programer/)
[写给前端工程师的10条实用原则](https://blog.fundebug.com/2018/08/29/10-things-you-will-eventually-learn-about-js-projects/)
[突破自己的技术思维](https://blog.fundebug.com/2019/02/26/about-technology-trap/)

## 基础
[React入门看这篇就够了](https://blog.fundebug.com/2019/06/10/react-complete-tutorial/)
[JavaScript函数式编程究竟是什么?](https://blog.fundebug.com/2019/08/07/javascript-functional-programing-introduction/)
[还不会正则表达式？看这篇！](https://blog.fundebug.com/2019/06/19/regular-expression-tutorial/)
[掌握 Async/Await](https://blog.fundebug.com/2019/05/08/master-async-await/)
[前端开发者必备的Nginx知识](https://blog.fundebug.com/2019/06/13/nginx-knowledge-for-frontend/)
[如何使用 Set 来提高JS代码的性能](https://blog.fundebug.com/2019/07/12/speedup-javascript-use-set/)
[JavaScript中的递归](https://blog.fundebug.com/2017/06/14/all-about-recursions/)
[你所不知道的JSON.stringify](https://blog.fundebug.com/2017/08/17/what-you-didnt-know%20about-json-stringify/)
[每个JavaScript工程师都应懂的33个概念](https://blog.fundebug.com/2018/10/30/33-js-concepts/)
[如何给localStorage设置一个过期时间？](https://blog.fundebug.com/2018/11/26/set-expire-time-for-localstorage/)
[抛弃console.log()，拥抱浏览器Debugger](https://blog.fundebug.com/2018/12/11/stop-using-console-log/)
[九种跨域方式实现原理（完整版）](https://blog.fundebug.com/2019/01/28/9-ways-of-cross-origin/)
[JavaScript 为什么要有 Symbol 类型？](https://blog.fundebug.com/2019/03/19/why-does-javascript-need-symbol/)
[分享下写技术文章的思路](https://blog.fundebug.com/2018/09/29/how-to-write-technology-blog/)

## 进阶

[JavaScript是如何工作的:渲染引擎和优化其性能的技巧](https://segmentfault.com/a/1190000017872125#articleHeader0)
[JS引擎是如何工作的？从调用堆栈到Promise](https://blog.fundebug.com/2019/07/02/javascript-from-callback-to-promise/)
[详解JavaScript的任务、微任务、队列以及代码执行顺序](https://blog.fundebug.com/2019/07/25/tasks-microtasks-queues-and-schedules/)
[JavaScript正则表达式进阶指南](https://blog.fundebug.com/2018/05/02/advanced_regular_expression/)
[JavaScript复杂判断的更优雅写法](https://blog.fundebug.com/2018/11/08/elegant-way-of-writing-if-in-javascript/)
[JavaScript如何工作:内存管理+如何处理4个常见的内存泄漏](https://blog.fundebug.com/2018/12/18/how-does-javascript-manage-memory/)
[浏览器缓存机制](https://blog.fundebug.com/2019/01/08/browser-cache-mechanism/)
[JavaScript是如何工作的：CSS和JS动画底层原理及如何优化它们的性能](https://blog.fundebug.com/2019/01/18/understand-css-and-javascript-animations/)
[如何优雅地查看 JS 错误堆栈？](https://blog.fundebug.com/2019/03/08/how-to-check-javascript-stacktrace/)
[深入了解浏览器存储：对比Cookie、LocalStorage、sessionStorage与IndexedDB](https://blog.fundebug.com/2019/04/08/about-browser-storage/)
[ESLint 工作原理探讨](https://blog.fundebug.com/2019/05/22/understand-eslint/)

## 性能

[全面分析前端的网络请求方式](https://blog.fundebug.com/2019/05/30/methods-to-initiate-http-request-of-frontend/)
[JavaScript 是如何工作的：JavaScript 的共享传递和按值传递](https://blog.fundebug.com/2019/04/18/master-javascript-call-by-sharing-parameter-passing/)
[Web 性能优化：Preload与Prefetch的使用及在 Chrome 中的优先级](https://blog.fundebug.com/2019/04/11/understand-preload-and-prefetch/)
[Web 性能优化： 使用 Webpack 分离数据的正确方法](https://blog.fundebug.com/2019/03/04/webpack-bundle-split/)
[WEB 实时推送技术的总结](https://blog.fundebug.com/2019/03/14/real-time-communication-technologies-of-web/)

## 技术储备
[WebAssembly的前世今身](https://blog.fundebug.com/2019/06/06/about-webassembly/)
[JavaScript是如何工作的：Web Workers的构建块 + 5个使用他们的场景](https://blog.fundebug.com/2019/01/02/understand-web-workes/)
[JavaScript 是如何工作的：WebRTC和对等网络的机制！](https://blog.fundebug.com/2019/01/30/understand-webrtc/)
[前端异常监控解决方案研究](https://blog.fundebug.com/2019/08/29/frontend-exception-monitor-research/)
[JavaScript是如何工作：Shadow DOM的内部结构 + 如何编写独立的组件！](https://blog.fundebug.com/2019/01/29/understand-shadow-dom/)
[漫淡终端技术未来](https://blog.fundebug.com/2018/12/14/about-the-future-of-frontend/)






















