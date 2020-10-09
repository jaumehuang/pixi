<!--
 * @Author: your name
 * @Date: 2020-09-30 16:10:24
 * @LastEditTime: 2020-10-09 22:01:13
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \pixi\src\page\index.vue
-->
<template>
  <div>
  <div class="loading" id="loading">加载中0%</div>
   <!-- <img src="../img2/01.jpg" style="width:100%"/> <-->
  </div>
  
  
</template>
<script>
import * as PIXI from 'pixi.js'
let Application = PIXI.Application,
    Container = PIXI.Container,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Sprite = PIXI.Sprite;
const pd = 1800;
export default {
  data() {
    return {
      scenes:[
        {
          name:"01",
          x:0,
          y:0,
          width:"800",
          height:"1800"
        },
        {
          name:"02",
          x:0,
          y:pd*1,
          width:"800",
          height:"1800"
        },
        {
          name:"03",
          x:0,
          y:pd*2,
          width:"800",
          height:"1800"
        },
        {
          name:"04",
          x:0,
          y:pd*3,
          width:"800",
          height:"1800"
        },
         {
          name:"05",
          x:0,
          y:pd*4,
          width:"800",
          height:"1800"
        },
         {
          name:"06",
          x:0,
          y:pd*5,
          width:"800",
          height:"1800"
        },
         {
          name:"07",
          x:0,
          y:pd*6,
          width:"800",
          height:"1800"
        },
         {
          name:"08",
          x:0,
          y:pd*7,
          width:"800",
          height:"1800"
        },
         {
          name:"09",
          x:0,
          y:pd*8,
          width:"800",
          height:"1800"
        },
         {
          name:"10",
          x:0,
          y:pd*9,
          width:"800",
          height:"1800"
        },
         {
          name:"11",
          x:0,
          y:pd*10,
          width:"800",
          height:"1800"
        },
         {
          name:"12",
          x:0,
          y:pd*11,
          width:"800",
          height:"1800"
        }
      ]
    };
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
    let app = new Application({ 
        width:w,
        height:9000,                      
        antialiasing: true, 
        transparent: true, 
        resolution: 1,
        backgroundColor: 0x1d9ce0,
      }
    );
    document.body.appendChild(app.view);
     // 获取屏幕宽高，判断横屏还是竖屏
    let min = (w < h) ? w : h;
    let scale = min / 750;  // 根据设计稿尺寸进行缩放比例调整
    app.stage.scale.set(scale, scale);  // 根据屏幕实际宽高放大舞台
    let max = (w > h) ? w : h;
    let scrollDis = app.stage.width - max
    console.log(scrollDis)
    //导入资源
    loader
    .add('01',require("../img2/01.jpg"))
    .add('02',require("../img2/02.jpg"))
    .add('03',require("../img2/03.jpg"))
    .add('04',require("../img2/04.jpg"))
    .add('05',require("../img2/05.jpg"))
    .add('06',require("../img2/06.jpg"))
    .add('07',require("../img2/07.jpg"))
    .add('08',require("../img2/08.jpg"))
    .add('09',require("../img2/09.jpg"))
    .add('10',require("../img2/10.jpg"))
    .add('11',require("../img2/11.jpg"))
    .add('12',require("../img2/12.jpg"))
    .load(setup)
    //进度加载
    loader.onProgress.add((target)=>{
      document.getElementById("loading").innerText = parseInt(target.progress) + "%";
    })
    //加载完成
    loader.onComplete.add((target)=>{
      document.getElementById('loading').style.display = 'none';
    })
    console.log(resources)
    let that =this;
    function setup(){

           that.scenes.forEach((item)=>{
             let scene = new Sprite.from(resources[item.name].texture);
                 scene.width=item.width;
                 scene.height=item.height;
              let sceneContainer = new Container({
                width:item.width,
                height:item.height
              });
              sceneContainer.addChild(scene);
              sceneContainer.x=item.x;
              sceneContainer.y=item.y;
              app.stage.addChild(sceneContainer);
           })
           return false;
            // let boy = new Sprite(resources['bed_boy'].texture);
            let boy = Sprite.from(resources['bed_boy'].texture);
            // boy.anchor.set(0.5);//设定中心锚点为中间
            boy.width = 800;//将位置设置为中间
            boy.height =1800;
           // app.stage.addChild(tow);//将精灵贴图放进舞台中
            let boyContainer = new Container(
            );
            boyContainer.addChild(boy);
            app.stage.addChild(boyContainer);

            let bed = Sprite.from(resources['bed'].texture);
            // boy.anchor.set(0.5);//设定中心锚点为中间
            bed.width = 800;//将位置设置为中间
            bed.height = 1800;
           // app.stage.addChild(tow);//将精灵贴图放进舞台中
            let bedContainer = new Container(
            );
            bedContainer.addChild(bed);
            app.stage.addChild(bedContainer);
            bedContainer.position.set(0,1800);
            // app.ticker.add(() => {
            //   // 每秒调用该方法60次(60帧动画)
            //   boy.rotation += 0.06;
            // })
         }
            new AlloyTouch({
            touch: "body", // 反馈触摸的dom
            //vertical: vertical, // 不必需，默认是true代表监听竖直方向touch
           // min:-scrollDis, // 不必需,运动属性的最小值
            maxSpeed: 1,
           // max: 0, // 不必需,滚动属性的最大值
            bindSelf: false,
            initialValue: 0,
            change: function (value) {
              console.log(value)
              if(value>-3900){
                app.stage.position['y'] = value;
              }
              
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