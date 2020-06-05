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




## 性能开发原则及说明

[[_TOC_]]

### 1. 页面加载性能

#### 1.1 优化资源大小

为提供卓越的性能，我们需要优化每一个字节的传送。通过优化资源的大小，显著降低资源的传输量，提高页面打开速度。

#### 1.2 避免不必要的冗余资源

检查冗余资源，可以遵循下面几点

- 清理网页上的本站资源和第三方资源
- 评估每个资源的作用、性能和价值
- 确定这些资源是否充分发挥其价值

可以通过 grunt、gulp、webpack 合并资源并使用 rollup 或者 tree-shaking 技术 消除没有用到的代码。

#### 1.3 优化文本资源的编码和传输

除了避免不必要的资源下载，在提高网页加载速度上您可以采取的最有效措施
就是，通过优化和压缩其余资源来最大限度减少总下载大小。

- 数据压缩概述

在您消除了任何不必要的资源之后，下一步就是对浏览器需要下载的其余资源
进行压缩。根据资源类型(文本、图像、字体等)，有若干不同的技术可供您
驱使:可在服务器上启用的通用工具、适用于特定内容类型的预处理优化以及
需要开发者输入的资源特定优化。

- 实现最佳性能需要组合使用上述所有技术。

  - 压缩就是使用更少的字节对信息进行编码的过程。
  - 消除不必要的数据总是会产生最好的结果。
  - 有许多种不同的压缩技术和算法。
  - 要利用各种技术来实现最佳压缩。

减小数据大小的过程称为数据压缩。许多人终其一生致力于算法、技术和优化研究，以期提高各种压缩程序的压缩比率、速度和内存要求。对数据压缩进行详细讨论超出了本主题的范围。但是，概要了解压缩的工作原理以及在减小网
页所需各类资源大小方面可供我们利用的技术，仍具有重要意义。

- 源代码压缩

  - 去除源码中不需要的空格和换行符
  - 使用 uglifyjs 等工具进行代码级别的字符替换压缩
  - 使用特定工具对 CSS、JS 和 HTML 源码进行压缩

- 数据传输压缩:通过 GZIP 压缩文本
  - GZIP 对基于文本的资源的压缩效果最好:CSS、JavaScript 和 HTML。
  - 所有现代浏览器都支持 GZIP 压缩，并且会自动请求该压缩。
  - 服务器必须配置为启用 GZIP 压缩。
  - 某些 CDN 需要特别注意以确保 GZIP 已启用。

GZIP 是一种可以作用于任何字节流的通用压缩程序。它会在后台记忆一些之 前看到的内容，并尝试以高效方式查找并替换重复的数据片段。(欲知详情， 请参阅浅显易懂的 GZIP 低阶说明。)但实际上，GZIP 对基于文本的内容的 压缩效果最好，在压缩较大文件时往往可实现高达 70-90% 的压缩率，而如果 对已经通过替代算法压缩过的资源(例如，大多数图片格式)运行 GZIP，则 效果甚微，甚至毫无效果。

#### 1.4 图片优化

图像通常占据了网页上下载字节的大部分，通常也占据了大量的视觉空间。因
此，优化图像通常可以最大限度地减少从网站下载的字节数以及提高网站性
能:浏览器需要下载的字节越少，占用客户端的带宽就越少，浏览器下载并在
屏幕上渲染有用内容的速度就越快。

- 删除和替换图像
  - 删除不需要的图片，使用 CSS 替代图片效果。
  - 尽可能的使用 CSS3 中的变换效果，替代不同特效的多余图片。
  - 使用字体图标替代图片资源，能大幅减小图标资源大小。

- 合并多个小图片(雪碧图)

使用 CSS Sprites 技术将多个小图片合并到一张大图中，使用 CSS 切割并获取 其中的图片，能够有效的降低图片资源加载数量，提高整体网页加载性能。

- 矢量图和位图
  - 使用矢量图替代简单的高分辨率图片
  - 使用矢量图做网页的图片自适应
  - 使用矢量图展示简单几何图形
  - 使用位图展示复杂无规律图片

- 使用 SVG
  - SVG 是一种基于 XML 的图片格式
  - SVG 文件应进行缩减，以减小其大小
  - SVG 文件应使用 GZIP 进行压缩

所有现代浏览器都支持可缩放矢量图形 (SVG)，这种基于 XML 的图片格式适 用于二维图形:我们可以将 SVG 标记直接嵌入网页，也可将其作为外部资源 嵌入网页。然后，可通过大多数基于矢量的绘图软件创建一个 SVG 文件，或 直接在您喜欢的文本编辑器中手动创建。

举个有说服力的例子，svgo 能够将由 Illustrator 生成的 SVG 文件的大小减 少 58%，使其从 470 个字节缩小到 199 个字节。而且，由于 SVG 是一种 基于 XML 的格式，因此我们还可以应用 GZIP 压缩来减小其传送大小 - 确 保将您的服务器配置为对 SVG 资源进行压缩。

- 无损图像压缩与有损图像压缩
  - 由于人眼的工作方式的缘故，对图像进行有损压缩是不错的选择-
  - 图像优化依赖有损和无损压缩来实现。
  - 图片格式上的差异是由于优化图像时使用的有损和无损算法的差异和使用方式的差异所致。
  - 并不存在任何适用于所有图像的最佳格式或“质量设置”:每个特定压缩程序与图像内容的组合都会产生独特的输出。

- 选择合适的图片格式
  - 首先选择正确的通用格式:GIF、PNG、JPEG。
  - 通过试验选出每一种格式的最佳设置:质量、调色板大小等。
  - 考虑为现代浏览器添加 WebP 和 JPEG XR 图片资源


除了不同的有损和无损压缩算法外，不同的图片格式还支持不同的功能，例如 动画和透明度 (alpha) 通道。因此，需要将所需视觉效果与功能要求相结合来 为特定图像选择“正确的格式”。


格式 | 透明度 | 动画 |  浏览器
--- | --- | --- | ---
GIF | 支持 | 支持 | 所有
PNG | 支持 | 不支持 | 所有
JPEG | 不支持 | 不支持 | 所有
JPEG XR | 支持 | 支持 | IE
WBEP | 支持 | 支持 | Chrome、Opera、Android、IOS

- 您是否需要动画?如果需要，GIF 是唯一的通用选择。
  - GIF 将调色板限制为最多 256 色，这对大多数图像而言都不是好的选择。 况且，对于调色板较小的图像，PNG-8 的压缩效果更佳。因此，只有需要 动画时，GIF 才是正确的选择。

- 您是否需要使用最高分辨率保留精细的细节?请使用 PNG。
  - 除了选择调色板的大小外，PNG 不采用任何有损压缩算法。因此，它能生 成最高质量的图像，但代价是文件大小要比其他格式大得多。请谨慎使 用。如果图像资源包含由几何形状组成的图像，请务必考虑将其转换成矢 量 (SVG) 格式!如果图像资源包含文本，请停下来再做考虑。图像中的文 本无法选择、搜索或“缩放”。如果您需要表现一种自定义外观(出于品牌推 广或其他原因)，请改用网页字体。

- 您是否要优化照片、屏幕截图或类似的图像资源?请使用 JPEG。
  - JPEG 组合使用有损和无损优化来减小图像资源的文件大小。请尝试几种JPEG 质量级别，为您的资源找到最佳的质量与文件大小平衡点。

由于 WebP 和 JPEG XR 均未得到普遍支持，您需要向应用或服务器添加额
外的逻辑来提供相应的资源:

- 有些 CDN 将图像优化作为一项服务提供，包括提供 JPEG XR 和 WebP。
- 有些开源工具(例如 PageSpeed for Apache 或 PageSpeed for Nginx) 自动优化、转换和提供相应资源。
- 您可以添加额外的应用逻辑来检测客户端，检查客户端支持的格式，并提 供最合适的图片格式。

- 使用工具压缩图片资源

没有任何一种图片格式、工具或优化参数集完美到适用于所有图像。为获得最
佳效果，您需要根据图像的内容及其视觉以及其他技术要求来挑选格式及其设
置。

工具 | 说明
--- | ---
gifsicle | 创建和优化 GIF 图像
jpegtran | 优化 JPEG 图像
optipng | 无损 PNG 优化
pngquant | 有损 PNG 优化

- 提供特定缩放的图片资源
  - 提供缩放的资源是最简单并且最有效的优化之一
  - 密切关注较大的资源，因为它们会产生大量开销
  - 通过将图像缩放到其显示尺寸，减少多余的像素
  - 为不同分辨率的客户端(电脑、手机、平板)提供各自最佳分辨率的图像

图像优化可归结为两个标准:优化编码每个图像像素所使用的字节数，和优化 总像素数:图像的文件大小就是总像素数与编码每个像素所使用字节数的乘 积。因此，最简单也是最有效的一种图像优化方法就是，确保我们提供的像素 数恰好是在浏览器中按预期尺寸显示资源所需的像素数。但大多数网页的许多图像资源都做不到这一点:它们提供的资源 通常较大，需要依赖浏览器对其进行重新缩放(这还会占用额外的 CPU 资 源)并以较低分辨率显示。

- 图像优化总结

  - 首选矢量格式:矢量图像与分辨率和缩放无关，这使它们成为多设备和高 分辨率情况的完美选择。
  - 缩小和压缩 SVG 资源: 大多数绘图应用程序生成的 XML - 标记往往包 含可以移除的多余元数据;确保您的服务器配置为对 SVG 资源采用 GZIP 压缩。
  - 挑选最佳位图格式:确定您的功能要求并选择适合每个特定资源的格式。
  - 通过试验为位图找到最佳质量设置:不要害怕调低“质量”设置，调低后的效 果通常很不错，并且大小的缩减很显著。
  - 移除多余的图像元数据:许多位图都包含多余的资源元数据:地理信息、 相机信息等。请使用合适的工具删除这些数据。
  - 提供缩放的图像:调整服务器上的图像尺寸，并确保图像的“显示”尺寸尽可 能接近其“自然”尺寸。尤其要密切注意较大的图像，因为在调整尺寸时，它 们占用的开销最大。
  - 自动化:部署自动化工具和基础设施，这样可以确保您的所有图像资源始 终得到优化。

#### 1.5 HTTP 缓存

通过网络获取内容既速度缓慢又开销巨大。较大的响应需要在客户端与服务器
之间进行多次往返通信，这会延迟浏览器获得和处理内容的时间，还会增加访
问者的流量费用。因此，缓存并重复利用之前获取的资源的能力成为性能优化
的一个关键方面。

好在每个浏览器都自带了 HTTP 缓存实现功能。您只需要确保每个服务器响 应都提供正确的 HTTP 标头指令，以指示浏览器何时可以缓存响应以及可以 缓存多久。

如果您在应用中使用 Webview 来获取和显示网页内容，可能需要提供额外的 配置标志，以确保 HTTP 缓存得到启用、其大小根据用例进行了合理设置并 且缓存将持久保存。

##### 通过 ETag 验证缓存的响应

- 服务器使用 ETag HTTP 标头传递验证令牌。
- 验证令牌可实现高效的资源更新检查:资源未发生变化时不会传送任何数
据。

假定在首次获取资源 120 秒后，浏览器又对该资源发起了新的请求。首先， 浏览器会检查本地缓存并找到之前的响应。遗憾的是，该响应现已过期，浏览 器无法使用。此时，浏览器可以直接发出新的请求并获取新的完整响应。不 过，这样做效率较低，因为如果资源未发生变化，那么下载与缓存中已有的完 全相同的信息就毫无意义。

这正是验证令牌(在 ETag 标头中指定)旨在解决的问题。服务器生成并返回 的随机令牌通常是文件内容的哈希值或某个其他指纹。客户端不需要了解指纹 是如何生成的，只需在下一次请求时将其发送至服务器。如果指纹仍然相同， 则表示资源未发生变化，您就可以跳过下载。

##### Cache-Control

- 每个资源都可通过 Cache-Control HTTP 标头定义其缓存策略
- Cache-Control 指令控制谁在什么条件下可以缓存响应以及可以缓存多久。
- 从性能优化的角度来说，最佳请求是无需与服务器通信的请求:您可以通
过响应的本地副本消除所有网络延迟，以及避免数据传送的流量费用。为 实现此目的，HTTP 规范允许服务器返回 Cache-Control 指令，这些指令 控制浏览器和其他中间缓存如何缓存各个响应以及缓存多久。

注:Cache-Control 标头是在 HTTP/1.1 规范中定义的，取代了之前用来定义 响应缓存策略的标头(例如 Expires)。所有现代浏览器都支持 Cache- Control，因此，使用它就足够了。

##### “no-cache”和“no-store”

“no-cache”表示必须先与服务器确认返回的响应是否发生了变化，然后才能使 用该响应来满足后续对同一网址的请求。因此，如果存在合适的验证令牌 (ETag)，no-cache 会发起往返通信来验证缓存的响应，但如果资源未发生变 化，则可避免下载。

相比之下，“no-store”则要简单得多。它直接禁止浏览器以及所有中间缓存存储 任何版本的返回响应，例如，包含个人隐私数据或银行业务数据的响应。每次 用户请求该资源时，都会向服务器发送请求，并下载完整的响应。

##### “public”与“private”

如果响应被标记为“public”，则即使它有关联的 HTTP 身份验证，甚至响应状 态代码通常无法缓存，也可以缓存响应。大多数情况下，“public”不是必需的， 因为明确的缓存信息(例如“max-age”)已表示响应是可以缓存的。

相比之下，浏览器可以缓存“private”响应。不过，这些响应通常只为单个用户 缓存，因此不允许任何中间缓存对其进行缓存。例如，用户的浏览器可以缓存 包含用户私人信息的 HTML 网页，但 CDN 却不能缓存。

##### “max-age”

指令指定从请求的时间开始，允许获取的响应被重用的最长时间(单位: 秒)。例如，“max-age=60”表示可在接下来的 60 秒缓存和重用响应。

##### 定义最佳 Cache-Control 策略

Cache-Control 指令和说明

指令 | 说明
---|---
max-age=86400 | 浏览器以及任何中间缓存均可将响应(如果是 “public”响应)缓存长达 1 天(60 秒 x 60 分钟 x 24 小时)。
private, max-age=600 | 客户端的浏览器只能将响应缓存最长 10 分钟(60 秒 x 10 分钟)。
no-store | 不允许缓存响应，每次请求都必须完整获取。

根据 HTTP Archive，在排名最高的 300,000 个网站(按照 Alexa 排名) 中，所有下载的响应中几乎有半数可由浏览器缓存，这可以大量减少重复的网 页浏览和访问。当然，这并不意味着您的特定应用有 50% 的资源可以缓存。 一些网站的资源 90% 以上都可以缓存，而其他网站可能有许多私密或时效要 求高的数据根本无法缓存。
请审核您的网页，确定哪些资源可以缓存，并确保它们返回正确的 Cache- Control 和 ETag 标头。

##### 废弃和更新缓存的响应

- 在资源“过期”之前，将一直使用本地缓存的响应。
- 您可以通过在网址中嵌入文件内容指纹，强制客户端更新到新版本的响应。
- 为获得最佳性能，每个应用都需要定义自己的缓存层次结构。

浏览器发出的所有 HTTP 请求会首先路由到浏览器缓存，以确认是否缓存了 可用于满足请求的有效响应。如果有匹配的响应，则从缓存中读取响应，这样 就避免了网络延迟和传送产生的资源下载时间。

不过，如果需要更新或废弃缓存的响应，该怎么办?例如，假定您已告诉访问 者将某个 CSS 样式表缓存长达 24 小时 (max-age=86400)，但设计人员刚刚 提交了一个您希望所有用户都能使用的更新。您该如何通知拥有现在“已过时” 的 CSS 缓存副本的所有访问者更新其缓存?在不更改资源网址的情况下，您 做不到。

浏览器缓存响应后，缓存的版本将一直使用到过期(由 max-age 或 expires 决定)，或一直使用到由于某种其他原因从缓存中删除，例如用户清除了浏览 器缓存。因此，构建网页时，不同的用户可能最终使用的是文件的不同版本; 刚获取了资源的用户将使用新版本的响应，而缓存了早期(但仍有效)副本的 用户将使用旧版本的响应。

所以，如何才能鱼和熊掌兼得:客户端缓存和快速更新?您可以在资源内容发生变化时更改它的网址，强制用户下载新响应。通常情况下，可以通过在文件名中嵌入文件的指纹或版本号来实现。

因为能够定义每个资源的缓存策略，所以您可以定义“缓存层次结构”，这样不 但可以控制每个响应的缓存时间，还可以控制访问者看到新版本的速度。

- HTML 被标记为“no-cache”，这意味着浏览器在每次请求时都始终会重新 验证文档，并在内容变化时获取最新版本。此外，在 HTML 标记内，您在 CSS 和 JavaScript 资源的网址中嵌入指纹:如果这些文件的内容发生变 化，网页的 HTML 也会随之改变，并会下载 HTML 响应的新副本。
- 允许浏览器和中间缓存(例如 CDN)缓存 CSS，并将 CSS 设置为 1 年 后到期。请注意，您可以放心地使用 1 年的“远期过期”，因为您在文件名 中嵌入了文件的指纹:CSS 更新时网址也会随之变化。
- JavaScript 同样设置为 1 年后到期，但标记为 private，这或许是因为它 包含的某些用户私人数据是 CDN 不应缓存的。
- 图像缓存时不包含版本或唯一指纹，并设置为 n 天后到期。

可以组合使用 ETag、Cache-Control和唯一网址来实现一举多得:较长的过期时间、控制可以缓存响应的位置以及随需更新。

##### HTTP 缓存总结

HTTP 缓存不存在最佳缓存策略。需要根据通信模式、提供的数据类型以及应 用特定的数据更新要求，为每个资源定义和配置合适的设置，以及整体的“缓存 层次结构”。

在制定缓存策略时，需要牢记下面这些技巧和方法:

- 使用一致的 URL:如果您在不同的URL上提供相同的内容，将会多次获取 和存储这些内容。提示:请注意，URL 区分大小写。
- 确保服务器提供验证令牌(ETag):有了验证令牌，当服务器上的资源未发 生变化时，就不需要传送相同的字节。
- 确定中间缓存可以缓存哪些资源:对所有用户的响应完全相同的资源非常 适合由 CDN 以及其他中间缓存进行缓存。为每个资源确定最佳缓存周 期:不同的资源可能有不同的更新要求。为每个资源审核并确定合适的 max-age。
- 确定最适合您的网站的缓存层次结构:您可以通过为 HTML 文档组合使用 包含内容指纹的资源网址和短时间或 no-cache 周期，来控制客户端获取 更新的速度。
- 最大限度减少文件耦合:某些资源的更新比其他资源频繁。如果资源的特 定部分(例如JavaScript函数或CSS样式集)会经常更新，可以考虑将 其代码作为单独的文件提供。这样一来，每次获取更新时，其余内容(例 如变化不是很频繁的库文件)可以从缓存获取，从而最大限度减少下载的 内容大小。


#### 1.6 HTTP/2

HTTP/2 的目的是通过支持完整的请求与响应复用来减少延迟，通过有效压缩 HTTP 标头字段将协议开销降至最低，同时增加对请求优先级和服务器推送的 支持。为达成这些目标，HTTP/2 还给我们带来了大量其他协议层面的辅助实 现，例如新的流控制、错误处理和升级机制。上述几种机制虽然不是全部，但 却是最重要的，每一位网络开发者都应该理解并在自己的应用中加以利用。

HTTP/2 没有改动 HTTP 的应用语义。HTTP 方法、状态代码、URI 和标头 字段等核心概念一如往常。不过，HTTP/2 修改了数据格式化(分帧)以及在 客户端与服务器间传输的方式。这两点统帅全局，通过新的分帧层向我们的应 用隐藏了所有复杂性。因此，所有现有的应用都可以不必修改而在新协议下运 行。

为了实现 HTTP 工作组设定的性能目标，HTTP/2 引入了一个新的二进制分帧 层，该层无法与之前的 HTTP/1.x 服务器和客户端向后兼容，因此协议的主版 本提升到 HTTP/2。

即便如此，除非您在实现网络服务器(或自定义客户端)，需要使用原始的 TCP 套接字，否则您很可能注意不到任何区别:所有新的低级分帧由客户端和 服务器为您执行。可观察到的唯一区别将是性能的提升和请求优先级、流控制 与服务器推送等新功能的出现。

##### HTTP/2.0 优势

HTTP/2.0 起源于 Google 开放的 SPDY 协议，在此协议上做了进一步的优化。 新的二进制帧

HTTP/1.x 诞生的时候是明文协议，其格式由三部分组成:start line(request line 或者 status line)，header，body。要识别这 3 部分就要做协议解析， HTTP/1.x 的解析是基于文本。基于文本协议的格式解析存在天然缺陷，文本的 表现形式有多样性，要做到健壮性考虑的场景必然很多，二进制则不同，只认 0 和 1 的组合。基于这种考虑 HTTP/2.0 的协议解析决定采用二进制格式，实 现方便且健壮。

HTTP/2.0 的格式定义更接近 tcp 层的方式，这张二机制的方式十分高效且精 简。length 定义了整个 frame 的开始到结束，type 定义 frame 的类型(一共 10 种)，flags 用 bit 位定义一些重要的参数，stream id 用作流控制，剩下的 payload 就是 request 的正文了。

##### 多路复用

HTTP/2.0 要解决的一大难题就是多路复用(MultiPlexing)，即连接共享。上 面协议解析中提到的stream id就是用作连接共享机制的。一个 request 对应一 个 stream 并分配一个 id，这样一个连接上可以有多个 stream，每个 stream 的frame 可以随机的混杂在一起，接收方可以根据 stream id 将 frame 再归属到各 自不同的 request 里面。

多路复用通过多个请求 stream 共享一个 tcp 连接的方式，解决了 HTTP/1.x head of line blocking(排头阻塞)的问题，降低了延迟同时提高了带宽的利用 率。

请求优先级(request prioritization)。多路复用带来一个新的问题是，在连接 共享的基础之上有可能会导致关键请求被阻塞。HTTP/2.0 允许给每个 request 设置优先级，这样重要的请求就会优先得到响应。比如浏览器加载首页，首页 的 html 内容应该优先展示，之后才是各种静态资源文件，脚本文件等加载，这 样可以保证用户能第一时间看到网页内容。

参考对比网站 https://http2.akamai.com/demo 中，浏览器使用 HTTP/1.1 和 HTTP/2.0 方式分别请求 379 张图片作为对比。


##### 请求头压缩

在 HTTP/1.1 的 header 很多时候都是重复多余的。选择合适的压缩算法可以减 小包的大小和数量。HTTP2.0/SPDY 对 header 的压缩率可以达到 80%以上， 低带宽环境下效果很大。

在 HTTP/2.0 中使用专门设计的 HPACK(Header Compression for HTTP/2 RFC 7541)算法针对请求头进行压缩。

HTTP1.X 由于其设计的缺陷，被大家诟病已久，其中头疼的问题之一，就是 无意义的重复的头部。于是出现了各种各样的解决方案， 如 Google 直接在 HTTP1.X 的基础上设计了 SPDY 协议， 对头部使用 deflate 算法进行压 缩，一并解决了多路复用和优先级等问题。

HTTP/2.0 参考了 SPDY 协议，专门设计了 HPACK 算法，实际效果在大部分 请求头可以达到 80%的压缩率。

详细原理参考 http://http2.github.io/http2-spec/compression.html

### 2. 运行时性能

#### 2.1 优化渲染性能

#### 2.2 优化JavaScript执行效率

JavaScript 经常会触发视觉变化。有时是直接通过样式操作，有时是会产生视 觉变化的计算，例如搜索数据或将其排序。时机不当或长时间运行的 JavaScript 可能是导致性能问题的常见原因。您应当设法尽可能减少其影响。
JavaScript 性能分析可以说是一门艺术，因为您编写的 JavaScript 代码与实 际执行的代码完全不像。现代浏览器使用 JIT 编译器和各种各样的优化和技巧 来尝试为您实现尽可能快的执行，这极大地改变了代码的动态。
尽管如此，您肯定还是可以做一些事情来帮助您的应用很好地执行 JavaScript。

- 对于动画效果的实现，避免使用 setTimeout 或 setInterval，请使用 requestAnimationframe。
- 将长时间运行的 JavaScript 从主线程移到 Web Worker。
- 使用微任务来执行对多个帧的 DOM 更改。
- 使用 Chrome DevTools 的 Timeline 和 JavaScript 分析器来评估
JavaScript 的影响。

##### 降低复杂性或使用 Web Worker

JavaScript 在浏览器的主线程上运行，恰好与样式计算、布局以及许多情况下 的绘制一起运行。如果 JavaScript 运行时间过长，就会阻塞这些其他工作， 可能导致帧丢失。

因此，您要妥善处理 JavaScript 何时运行以及运行多久。例如，如果在滚动 之类的动画中，最好是想办法使 JavaScript 保持在 3-4 毫秒的范围内。超过 此范围，就可能要占用太多时间。如果在空闲期间，则可以不必那么斤斤计较 所占的时间。

在许多情况下，可以将纯计算工作移到 Web Worker，例如，如果它不需要 DOM 访问权限。数据操作或遍历(例如排序或搜索)往往很适合这种模型， 加载和模型生成也是如此。

并非所有工作都适合此模型:Web Worker 没有 DOM 访问权限。如果您的工 作必须在主线程上执行，请考虑一种批量方法，将大型任务分割为微任务，每 个微任务所占时间不超过几毫秒，并且在每帧的 requestAnimationframe 处理 程序内运行。

##### 使用 requestAnimationframe 来实现视觉变化

当屏幕正在发生视觉变化时，您希望在适合浏览器的时间执行您的工作，也就 是正好在帧的开头。保证 JavaScript 在帧开始时运行的唯一方式是使用 requestAnimationframe。
框架或示例可能使用 setTimeout 或 setInterval 来执行动画之类的视觉变化， 但这种做法的问题是，回调将在帧中的某个时点运行，可能刚好在末尾，而这 可能经常会使我们丢失帧，导致卡顿。

#### 2.3 降低 CSS 计算范围并降低其复杂性

通过添加和删除元素，更改属性、类或通过动画来更改 DOM，全都会导致浏 览器重新计算元素样式，在很多情况下还会对页面或页面的一部分进行布局 (即自动重排)。这就是所谓的计算样式的计算。
计算样式的第一部分是创建一组匹配选择器，这实质上是浏览器计算出给指定 元素应用哪些类、伪选择器和 ID。
第二部分涉及从匹配选择器中获取所有样式规则，并计算出此元素的最终样
式。

- 降低选择器的复杂性;使用以类为中心的方法，例如 BEM。
- 减少必须计算其样式的元素数量。

##### 降低选择器的复杂性

在最简单的情况下，您在 CSS 中引用只有一个类的元素:

````
.title {
/* styles */
}
````

但是，随着项目的增长，将可能产生更复杂的 CSS，最终您的选择器可能变成 这样:

````
.box:nth-last-child(-n+1) .title {
/* styles */
}
````

浏览器首先必须知道关于其他元素的所有情况，以及其后面是否有任何元素会 是第 N 个最后子元素，因为其类匹配，这可能比简单地将选择器与元素匹配 的开销要大得多。



##### 减少要计算样式的元素数量

另一个性能考虑，对于许多样式更新而言是更重要的因素，即减少在元素更改
时需要计算的工作量。
总体来说，计算元素的计算样式的最糟糕的开销情况是元素数量乘以选择器数
量，因为需要对照每个样式对每个元素都检查至少一次，看它是否匹配。
样式计算可能经常是直接针对少量元素，而不是声明整个页面无效。在现代浏
览器中，这往往不再是个问题，因为浏览器并不一定需要检查一项更改可能影
响的所有元素。另一方面，较早的浏览器不一定针对此类任务进行了优化。应
当尽可能减少声明为无效的元素的数量。

##### 使用块、元素、修饰符
BEM(块、元素、修饰符)之类的编码方法实际上纳入了上述选择器匹配的性 能优势，因为它建议所有元素都有单个类，并且在需要层次结构时也纳入了类 的名称:

````
.list { }
.list__list-item { }
````

如果需要一些修饰符，像在上面我们想为最后一个子元素做一些特别的东西，
就可以按如下方式添加:

````
.list__list-item--last-child {}
````


#### 2.4 避免布局抖动

布局是浏览器计算各元素几何信息的过程:元素的大小以及在页面中的位置。 根据所用的 CSS、元素的内容或父级元素，每个元素都将有显式或隐含的大小 信息。此过程在 Chrome、Opera、Safari 和 Internet Explorer 中称为布局 (Layout)。 在 Firefox 中称为自动重排 (Reflow)，但实际上其过程是一样的。
与样式计算相似，布局开销的直接考虑因素如下:

1. 需要布局的元素数量。
2. 这些布局的复杂性。

- 布局的作用范围一般为整个文档。
- DOM 元素的数量将影响性能;应尽可能避免触发布局。
- 评估布局模型的性能;新版 Flexbox 一般比旧版 Flexbox 或基于浮动的
布局模型更快。
- 避免强制同步布局和布局抖动;先读取样式值，然后进行样式更改。

##### 尽可能避免布局操作

当您更改样式时，浏览器会检查任何更改是否需要计算布局，以及是否需要更 新渲染树。对“几何属性”(如宽度、高度、左侧或顶部)的更改都需要布局计 算。

布局几乎总是作用到整个文档。 如果有大量元素，将需要很长时间来算出所有 元素的位置和尺寸。

使用 flexbox 而不是较早的布局模型

大多数情况下，使用 flexbox 布局能够比传统 css 布局有更好的性能和开发效
率。参考链接

https://developers.google.com/web/updates/2013/10/Flexbox-layout-isn-t-slow

##### 避免强制同步布局

首先 JavaScript 运行，然后计算样式，然后布局。但是，可以使用 JavaScript 强制浏览器提前执行布局。这被称为强制同步布局。

##### 避免布局抖动

有一种方式会使强制同步布局甚至更糟:接二连三地执行大量这种布局。看看
这个代码:

````
function resizeAllParagraphsToMatchBlockWidth() {
    // Puts the browser into a read-write-read-write cycle.
    for (var i = 0; i < paragraphs.length; i++) {
         paragraphs[i].style.width = box.offsetWidth + 'px';
    }
}
````

此代码循环处理一组段落，并设置每个段落的宽度以匹配一个称为“box”的元素 的宽度。这看起来没有害处，但问题是循环的每次迭代读取一个样式值 (box.offsetWidth)，然后立即使用此值来更新段落的宽度 (paragraphs[i].style.width)。在循环的下次迭代时，浏览器必须考虑样式已更改 这一事实，因为 offsetWidth 是上次请求的(在上一次迭代中)，因此它必须 应用样式更改，然后运行布局。每次迭代都将出现此问题。
此示例的修正方法还是先读取值，然后写入值:

````
// Read.
var width = box.offsetWidth;
function resizeAllParagraphsToMatchBlockWidth() {
    for (var i = 0; i < paragraphs.length; i++) {
         // Now write.
         paragraphs[i].style.width = width + 'px';
    }
}
````

#### 2.5 减少重绘、重排

##### 使用 CSS3 transform 和 opacity 属性更改来实现动画

尽量使用 CSS3 Transform 能够使布局和重绘的代价最小。

##### 提升打算设置动画的元素

应当将打算设置动画的元素(在合理范围内)提升到其自己的层:

````
.moving-element {
    will-change: transform;
}
````

或者，对于旧版浏览器，或者不支持 will-change 的浏览器:

````
.moving-element {
    transform: translateZ(0);
}
````

这可以提前警示浏览器即将出现更改，根据您打算更改的元素，浏览器可能可
以预先安排，如创建合成器层。

#### 2.6 输入事件节流（去除抖动）

输入事件可能是应用出现性能问题的原因，因为它们可能阻止帧完成，并且可
能导致额外(且不必要)的布局工作。

- 避免长时间反复触发事件;它们可能阻止滚动。
- 不要在事件处理程序中进行样式更改。
- 使处理程序去除抖动;存储事件值并在下一个 requestAnimationframe 回
调中处理样式更改。

##### 避免长时间反复触发事件

在最快的情况下，当用户与页面交互时，页面的合成器线程可以获取用户的触 摸输入并直接使内容移动。这不需要主线程执行任务，主线程执行的是 JavaScript、布局、样式或绘制。

但是，如果您附加一个输入处理程序，例如 touchstart、touchmove 或 touchend，则合成器线程必须等待此处理程序执行完成，因为您可能选择调用 preventDefault() 并且会阻止触摸滚动发生。即使没有调用 preventDefault()， 合成器也必须等待，这样用户滚动会被阻止，这就可能导致卡顿和漏掉帧。

总之，要确保您运行的任何输入处理程序应快速执行，并且允许合成器执行其
工作。

##### 避免在输入处理程序中更改样式

与滚动和触摸的处理程序相似，输入处理程序被安排在紧接任何 requestAnimationframe 回调之前运行。

如果在这些处理程序之一内进行视觉更改，则在 requestAnimationframe 开始 时，将有样式更改等待处理。如果按照“避免大型、复杂的布局和布局抖动”的建议，在 requestAnimationframe 回调开始时就读取视觉属性，将触发强制同 步布局。



















