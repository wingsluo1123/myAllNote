# Application for Harmony OS Next

## 组件部分

### 占全屏

```ArkTS
.expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
```

### 主轴

```
.justifyContent(FlexAlign.xx) // 使得column和row组件的主轴方向的内容排列整齐
```



### 交叉轴

与主轴垂直的另一条轴

```
.alignItem(xx.yy) // 使得column和row组件的交叉轴方向的内容排列整齐
// xx：当使用colmn组件时，取HorizonAlign, row取VerticalAlign
// yy：row取 顶中底，colmn取 左中右
```

### 自适应伸缩

给一个column或者row里的组件分配空间

```
.layoutWeight(x) // 如果只有这一个组件写了该函数，则剩余的空间全部归该组件，如果其他组件也写了该函数，那么按照x的比例来分配空间
```

### flex的wrap换行布局

```
@Entry                                  //@指的是装饰器
@Component                              //约定下方的代码是组件
struct Index {
  build() { //构建  一个build只能有一个容器跟组件，即下方的第一个Column
    Column(){
      Text('阶段选择')
        .fontWeight(700)
        .fontSize(40)
        .width('100%')
        .margin({top: 20, left: 20, bottom: 20})
      Flex({
      		// 主轴对齐方式 justifyContent
      		// 交叉轴对齐方式 alignItems
      		// 主轴方向 directoin 
        wrap: FlexWrap.Wrap, // 换行布局
      }){
        Text('arkts').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('arkUI').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('java').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('typescripts').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('arkts').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('arkUI').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('java').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
        Text('typescripts').backgroundColor(Color.Gray).padding(15).borderRadius(5).margin(5)
      }
    }
    .backgroundColor(Color.Pink)
    .padding({left: 10, right: 10})
    .height('100%')
    .width('100%')
    // .backgroundImage($r('app.media.jd_background'))
    // .backgroundImageSize(ImageSize.Cover)
    // .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    // .justifyContent(FlexAlign.SpaceBetween)
  }
}
```



## 案例

### 得物卡片

```
@Entry                                  //@指的是装饰器
@Component                              //约定下方的代码是组件
struct Index {
  build() { //构建  一个build只能有一个容器跟组件，即下方的第一个Column
    Column({space: 10}) {
      Row(){
        Column({space: 10}) {
          Text('玩一玩')
            .fontWeight(7)
            .fontSize(30)
          Text('签到兑礼 | 超多大奖 超好玩')
            .fontColor(Color.Gray)

        }
        .alignItems(HorizontalAlign.Start)

        Row() {
          Image($r('app.media.startIcon'))
            .height(80)
            .width(80)
            // .border({ width: 2 })
          Image($r('app.media.rightArrow'))
            .fillColor(Color.Gray)
            .height(40)
            // .border({ width: 2 })
        }
      }
      .backgroundColor(Color.Pink)
      .width('100%')
      .height(100)
      .padding(10)
      .justifyContent(FlexAlign.SpaceBetween)
      .borderRadius(10)

      Column({space: 10}){
        Image($r('app.media.HEART'))
          .height(300)
          .borderRadius(10)
        Column({space: 10}) {
          Text('今晚吃这个 | 每日艺术分享')
            .fontWeight(600)
            .fontSize(20)

          Text('No.43')
            .fontSize(20)
          Row() {
            Image($r('app.media.startIcon'))
              .borderRadius(20)
              .height(40)
              .width(40)
              .margin({right: 10})
            Text('插画师')
              .layoutWeight(1)
            Image($r('app.media.rightArrow'))
              .height(20)
              .width(20)
              .fillColor(Color.Gray)
            Text('2300')
          }
        }
        .alignItems(HorizontalAlign.Start)
      }
      .backgroundColor(Color.Pink)
      // .height(500) // 先定死一个高，写完内容后用内容撑开
      .width('100%')
      .borderRadius(10)
      .padding(10)
      .alignItems(HorizontalAlign.Start)
    }
    .padding(10)
    // .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    // .justifyContent(FlexAlign.SpaceBetween)
  }
}
```

### 京东登录

```
@Entry                                  //@指的是装饰器
@Component                              //约定下方的代码是组件
struct Index {
  build() { //构建  一个build只能有一个容器跟组件，即下方的第一个Column
    Column() {
      Row(){
       Text('退出')
         .layoutWeight(1)
          .fontWeight(600)
          .height(20)
          .width(20)
        Text('帮助')
          .fontWeight(600)
      }
      .width('100%')
      // .border({width: 2})

      Image($r('app.media.startIcon'))
        .height(170)
        .width(170)
        .margin(30)
        // .border({width: 2})

      TextInput({placeholder: '国家 / 地区'})
        .margin({bottom: 10})

      TextInput({placeholder: '请输入手机号'})
        .margin({bottom: 10})

      Button('登录')
        .width('100%')

      Row({space: 20}){
        Text('注册账号')
          .fontWeight(600)
        Text('密码登录')
          .fontWeight(600)
        Text('无法登录')
          .fontWeight(600)
      }
      .margin({top: 20})
      Row(){
        Checkbox()
        Text(){
          Span('我已阅读')
          Span('京东协议').fontColor(Color.Blue)
          Span('并同意')
        }

      }
      .margin({top: 20, bottom: 20})

      Blank() // 自动填充空白处

      Text('其他登录方式')
        .margin({bottom: 30})
      Row(){
        Column(){
          Image($r('app.media.startIcon'))
            .height(40)
            .width(40)
            .borderRadius(20)
          Text('华为登录')
        }

        Column(){
          Image($r('app.media.startIcon'))
            .height(40)
            .width(40)
            .borderRadius(20)
          Text('微信登录')
        }

        Column(){
          Image($r('app.media.startIcon'))
            .height(40)
            .width(40)
            .borderRadius(20)
          Text('QQ登录')
        }

      }
      .width('100%')
      .justifyContent(FlexAlign.SpaceEvenly)
      .margin({bottom: 20})
    }
    .backgroundColor(Color.Pink)
    .padding({left: 10, right: 10})
    .height('100%')
    .width('100%')
    // .backgroundImage($r('app.media.jd_background'))
    // .backgroundImageSize(ImageSize.Cover)
    // .expandSafeArea([SafeAreaType.SYSTEM], [SafeAreaEdge.TOP, SafeAreaEdge.BOTTOM])
    // .justifyContent(FlexAlign.SpaceBetween)
  }
}
```

