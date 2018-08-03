# FrontEnd MicroService Architecture

### 当前前端在复杂业务场景下的问题
- 项目庞大，维护成本居高不下
- 互联网企业产品快速迭代，技术层面为了加快研发进度牺牲了很多可维护性上的思考，导致项目很快就要面临完全重构的风险
- 技术繁多，招人困难，招进来的人需要重新适应新技术
- 使用iframe将部分模块嵌入到当前系统的方式可以解决部分问题。但是会引入包括无法与当前模块通信，加载重复资源的问题。而且需要设定好容器的样式与嵌入的页面向吻合
- 每一次修改都要重新部署整个应用，构建速度较慢。切容易引入不该发布的修改
- 多页应用。这是目前前端微服务的另一种实现方案，但是只能以整页的方式提供服务，而不能以单独模块提供

### 为什么要搞前端微服务
- 单个服务规模较小，易于维护
- 独立开发，独立部署互不干扰
- 服务间松耦合，没有依赖
- 技术栈不受限制
- 弹性伸缩

### 前端微服务的挑战
- 服务注册与服务订阅，目前没有现成方案
- 资源冲突，由于是多个独立的js甚至是css，目前的方案是独立的名字空间以及服务注册id，通过服务注册id来构建自己的微服务唯一的名字空间
- 

### 现有前端微服务技术方案

- The best solution I’ve seen is the [Single-SPA “meta framework”](https://github.com/CanopyTax/single-spa) to combine multiple frameworks on the same page without refreshing the page (see [this demo](https://single-spa.surge.sh/) that combines React, Vue, Angular 1, Angular 2, etc). See Bret Little’s explanation here.
- [Multiple single-page apps that live at different URLs](https://news.ycombinator.com/item?id=13011795). The apps use NPM/Bower components for shared functionality.
- Isolating micro-apps into [IFrames using libraries and Window.postMessage APIs to coordinate](https://news.ycombinator.com/item?id=13009285). IFrames share APIs exposed by their parent window.
- Make the different [modules communicate over a shared events bus](https://www.quora.com/Is-there-a-micro-service-architecture-approach-for-front-end-development/answer/Mohamed-Abdel-Maksoud-2) (e.g. [chrisdavies/eev](https://github.com/chrisdavies/eev)). Each module can be built using its own framework, as long as it handles incoming and outgoing events.
- Using [Varnish Cache to integrate different modules](http://allegro.tech/2016/03/Managing-Frontend-in-the-microservices-architecture.html).
- [Web Components as the integration layer](https://technologyconversations.com/2015/08/09/including-front-end-web-components-into-microservices/).
- [“Blackbox” React components](https://news.ycombinator.com/item?id=13012916).
