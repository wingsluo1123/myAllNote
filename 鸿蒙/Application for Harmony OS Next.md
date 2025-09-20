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

### 绝对定位和zIndex层级

.postion()使得组件的位置不再占用原来的位置，而是占用所填写坐标位置

.zIndex()中的参数位置越大，优先级越高，可以覆盖优先级低的组件。如果不写都不写zIndex，那么代码中越后面出现的组件，优先级越高。

```
Text('boss1')
        .height(50).width(50).backgroundColor(Color.Green)
      Text('boss2')
        .height(50).width(50).backgroundColor(Color.Yellow).position({x: 120, y: 30}).zIndex(1)
      Text('boss3')
        .height(50).width(50).backgroundColor(Color.White)
```

### 层叠布局

```
Stack({
        alignContent: Alignment.Bottom
      }){
        Text().height(250).width(250).backgroundColor(Color.White)
        Text().height(150).width(150).backgroundColor(Color.Blue)
        Text().height(50).width(50).backgroundColor(Color.Yellow)

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

### 人气卡片

```typescript
@Entry                                  //@指的是装饰器
@Component                              //约定下方的代码是组件
struct Index {
  build() { //构建  一个build只能有一个容器跟组件，即下方的第一个Column
    Column(){
      Column(){
        Image($r('app.media.HEART'))
          .height('50%')
          .width('100%')
          .borderRadius(25)
        Text('VIP')
          .height(25)
          .width(50)
          .backgroundColor(Color.Yellow)
          .fontColor(Color.Black)
          .fontWeight(600)
          // .padding({left: 10})
          .textAlign(TextAlign.Center)
          .fontStyle(FontStyle.Italic)
          .borderRadius({topLeft: 25, bottomRight: 25})
          .position({x: 0, y: 0})
        Row({space: 10}){
          Image($r('app.media.startIcon'))
            .height(40)
            .width(40)
            .borderRadius(20)
          Text('author')

        }
        .margin({top: 10})

      }
      .height(400 )
      .backgroundColor(Color.White)
      .borderRadius(10)
      .alignItems(HorizontalAlign.Start)
      .width(200)
      .border({width: 1})
      .padding(10)
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

### 支付宝界面

```typescript
@Entry                                  //@指的是装饰器
@Component                              //约定下方的代码是组件
struct Index {
  build() { //构建  一个build只能有一个容器跟组件，即下方的第一个Column
    // 1 整体stack布局 和 底部的tab
    Stack({alignContent: Alignment.Bottom}) {
      // 主体展示区
      Stack({alignContent: Alignment.Top}){
        // 头部
        Row(){
          Column(){
            Text('北京').fontSize(18).fontColor(Color.White)
            Text('晴 2℃').fontSize(12).fontColor(Color.White)
          }
          .margin({left: 10, right: 10})
          TextInput({placeholder: '搜索'}).height(40).width(230).backgroundColor(Color.White)
          Button('搜索')
            .margin({left: 5})
            .backgroundColor(Color.Gray)
        }
        .width('100%')
        .height(60)
        .backgroundColor('#5b73de')
        .zIndex(1)
        // 主体页面
        Scroll(){
          Column() {
            Row(){
              Column(){
                Image($r('app.media.startIcon')).height(20).width(20)
                Text('扫一扫')
              }
              .layoutWeight(1)
              Column(){
                Image($r('app.media.startIcon')).height(20).width(20)
                Text('余额')
              }
              .layoutWeight(1)
              Column(){
                Image($r('app.media.startIcon')).height(20).width(20)
                Text('收付款')
              }
              .layoutWeight(1)
            }
            .width('100%')
            .backgroundColor('#5b73de')

            Column({space: 10}){
                Row(){
                  Column(){
                    Image($r('app.media.startIcon'))
                      .height(30)
                      .width(30)
                      .borderRadius(10)
                    Text('嘀嘀打车')
                  }
                  .layoutWeight(1)
                  Column(){
                    Image($r('app.media.startIcon'))
                      .height(30)
                      .width(30)
                      .borderRadius(10)
                    Text('嘀嘀打车')
                  }
                  .layoutWeight(1)
                  Column(){
                    Image($r('app.media.startIcon'))
                      .height(30)
                      .width(30)
                      .borderRadius(10)
                    Text('嘀嘀打车')
                  }
                  .layoutWeight(1)
                }
                .margin({top: 10})

              Row(){
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
              }
              .margin({top: 10})

              Row(){
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
                Column(){
                  Image($r('app.media.startIcon'))
                    .height(30)
                    .width(30)
                    .borderRadius(10)
                  Text('嘀嘀打车')
                }
                .layoutWeight(1)
              }
              .margin({top: 10})

              Row({space: 10}){
                  Image($r('app.media.HEART'))
                    .height(200)
                    .width(100)
                    .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)
              }
              Row({space: 10}){
                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)
              }
              Row({space: 10}){
                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)

                Image($r('app.media.HEART'))
                  .height(200)
                  .width(100)
                  .borderRadius(10)
              }
            }
            .width('100%')
            .height('100%')
            .backgroundColor(Color.White)
            .borderRadius(20)
          }
          .height('100%')
          .width('100%')


        }
        .width('100%')
        .padding({top: 60, bottom: 60})
      }
      .width('100%')
      .height('100%')
      // 底部tab导航区
      Row(){
        Column(){
          Image($r('app.media.startIcon'))
            .width(35)
          Text('我的')
        }
        .layoutWeight(1)
        Column(){
          Image($r('app.media.startIcon'))
            .width(35)
          Text('首页')
        }
        .layoutWeight(1)
        Column(){
          Image($r('app.media.startIcon'))
            .width(35)
          Text('理财')
        }
        .layoutWeight(1)
      }
      .width('100%')
      .height(60)
      .backgroundColor('#fbfcfe')
    }
    .height('100%')
    .width('100%')
    .backgroundColor('#5b73de')
  }
}
```

