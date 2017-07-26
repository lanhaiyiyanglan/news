技术栈（vue2.0+axios+flex布局）
![image](https://github.com/lanhaiyiyanglan/news/blob/master/bb.gif)
用到的主要知识点有vue2.0的组件（注册使用，props传递数据，自定义事件），vue-router,外部插件的使用...
pages文件夹存放的是2个页面，主页和详情页（Home.vue和Detail.vue）
components文件夹存放的4个组件(详情页头部DetailHeader.vue,主页头部HomeHeader.vue,列表页1，列表页2）
主页引入swiper插件，以及头部和列表组件，banner和列表组件都通过axios获取json数据，banner获取的是外部数据，列表页获取本地data.json里的数据，列表页首次显示5条数据，每次下拉再显示5条，总数据20条，之后再下拉显示“没有数据了”
点击列表页，跳转到对应的详情页，详情页的数据线存放在router-link的params中，之后再通过$route.params获取

