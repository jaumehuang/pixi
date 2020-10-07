<!--
 * @Author: your name
 * @Date: 2020-09-30 16:10:24
 * @LastEditTime: 2020-10-07 12:29:36
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \pixi\src\page\index.vue
-->
<template>
  <div></div>
</template>
<script>
import {Application,Graphics,Sprite,Loader} from 'pixi.js'
import AlloyTouch from 'alloytouch'
import * as PIXI from 'pixi.js'
export default {
  data() {
    return {};
  },
  created() {
   
  },
  mounted() {
     this.initPixi();
  },
  methods: {
    /**
     * @describe: 初始化数据
     * @param {type}
     * @return {type}
     */
    initPixi() {
      const w = document.body.clientWidth;
      const  h = document.body.clientHeight; 
      const Container =PIXI.Container;
      const app = new PIXI.Application({
        width:w,
        height:800,
        antialias: true,
        transparent: false,
        resolution: 1,
        backgroundColor: 0x1d9ce0,
        antialiasing: true, 
    });
    document.body.appendChild(app.view);
   
    // 获取屏幕宽高，判断横屏还是竖屏
    let min = (w < h) ? w : h;
    let scale = min / 750;  // 根据设计稿尺寸进行缩放比例调整
    app.stage.scale.set(scale, scale);  // 根据屏幕实际宽高放大舞台

// 添加到app.stage里，从而可以渲染出来
  const loader = new PIXI.Loader();
    loader.add(require("../imgs/bed_boy.png"))
    .add(require("../imgs/bed.png"))
    .load(setup)
    // let tow2 = new Sprite(loader.resources[require("../imgs/bed.png")].texture);
    //     // tow2.anchor.set(0.5);//设定中心锚点为中间
    //     // tow2.x =500;//将位置设置为中间
    //     tow2.y = 1000;
    //        dd.stage.addChild(tow2);//将精灵贴图放进舞台中
    //进度加载
    loader.onProgress.add((target)=>{
      console.log('onProgress',target)
    })
    //加载完成
    loader.onComplete.add((target)=>{
      console.log('onComplete',target)
    })
        function setup(){
            let tow = new Sprite(loader.resources[require("../imgs/bed_boy.png")].texture);
            tow.anchor.set(0.5);//设定中心锚点为中间
            tow.x = app.screen.width/2;//将位置设置为中间
            tow.y = app.screen.height/2;
            app.stage.addChild(tow);//将精灵贴图放进舞台中
            
              const dd  = new Container()
              app.stage.addChild(dd);
              dd.stage.addChild(tow);//将精灵贴图放进舞台中
              return false
            app.ticker.add(() => {
              // 每秒调用该方法60次(60帧动画)
              tow.rotation += 0.06;
            })
         }
         this.initTouch();
        },
        //初始化滑动事件
        initTouch(vertical, val) {
          // let scrollDis = app.stage.width - max
           new AlloyTouch({
            touch: "body", // 反馈触摸的dom
            vertical:true, // 不必需，默认是true代表监听竖直方向touch
            min: -1, // 不必需,运动属性的最小值
            maxSpeed: 1,
            max: 0, // 不必需,滚动属性的最大值
            bindSelf: false,
            initialValue: 0,
            change: function (value) {
              // app.stage.position[val] = value;
              // let progress = -value / scrollDis;
              // progress = progress < 0 ? 0 : progress;
              // progress = progress > 1 ? 1 : progress;
              // timeline.seek(progress);
            }
          })
        }
  },
};
</script>