# fullscreen
##简介
简易整屏滚动插件
## 使用方式
###调用方式：
    var scroll = $.FullScreen({
        move: '.main-mod',
        row: '.row',
        nav: '.nav',
        time: '1s',
        type: 'cubic-bezier(1,-0.12, 0.44, 0.99)',
        navClass: 'cursor',
        minHeight: 200
    })

###参数列表:
|    参数      |   说明   |是否必需|
|------------------|----------|----------|
|move            | 运动元素  |是|
|row           | 每屏元素   |是|
| nav           | 导航元素 |是|
|wrap      | move元素外围包裹元素，没有的话默认body   | 否|
|allNum   | 屏幕总数量  | 否|
| time | 滚动时长 | 否|
|type       | 滚动效果 | 否|
| navClass         | 当前nav添加的class   |否|
|minHeight       | 最小高度，屏幕小于此高度平铺不滚动   | 否|
|normalHeight      | 平铺不滚屏时的屏默认高度   | 否|

###暴露的接口:
|      接口       |   说明   |参数|
|------------------|----------|------|
| pause            | 禁止滚动  |无|
| play            | 打开滚动   |无|
| changeMoveType | 改变滚动属性：时间或者滚动效果 | 一个只能包含'time'或'type'属性的对象|
| on        | 监听自定义事件 | 事件名称和listener|
| fire          | 触发自定义事件   |第一个参数为事件名称，后边所有参数推入一个数组当作数据|
| off         | 删除自定义事件   | 事件名称和listener|

###自定义事件:

    var aa = function(data) {
        //没有滚动时的处理（低级浏览器或者屏幕小于最低高度）
    }
    scroll.on('no-scroll', aa)
    
    scroll.on('ready-scroll', function(data) {
        console.log(data)  //['pre',1,2]
        //滚动触发时的处理
    })
    
    scroll.on('done-scroll', function(data) {
        //滚动结束时的处理
    })
    
    
    例子:
    //从第一屏滚动到第2屏后，改变此时以后的滚动时间为4s
     scroll.on('done-scroll', function(data) {
        if( data[1] === 1 && data[2] === 2){
            this.changeMoveType({
                time:'4s'
            })
        }
    })
    
##兼容性
不支持IE10以下浏览器

