<!--
 * @Author: your name
 * @Date: 2020-09-30 16:10:24
 * @LastEditTime: 2020-10-11 00:55:30
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \pixi\src\page\index.vue
-->
<template>
  <div id="longhua">
  <div class="loading" id="loading">加载中0%</div>
  <img src="../img2/01.jpg" class="dd" style="width:50px;position: absolute;left:0" height="50" width="50"/>
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
let timeline = new TimelineMax({
  paused: true
});
export default {
  data() {
    return {
      //场景数据
      scenesOptions:[
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
      ],
      scenesList:[],//场景集合
      //初始化精灵数据
      spritesOptions:[
        {
          bg01:{
             width:800,
             height:1800,
             position: { x: 0, y: 0 }
          },
          bg01Womam:{
             width:700,
             height:800,
             position: { x: 400, y: 640 }
          }
        },
        {
           bg02:{
             width:800,
             height:1800,
             position: { x: 0, y: 0 }
           }
        },
        {
           bg03:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           },
           bg03Postman:{
             width:464,
             height:600,
             position: { x: 0, y: 720 }
           }
        },
         {
           bg04:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           },
           bg04Professionalwomen:{
             width:664,
             height:800,
             position: { x:400, y:300 }
           }
        },
         {
           bg05:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           },
            bg05train:{
             width:1000,
             height:550,
            // rotation:-49,
             position: { x: -1000, y:-100 }
           }
        },
         {
           bg06:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           },
            bg06rail:{
             width:1000,
             height:520,
             position: { x:-700, y: -575 }
           }
        },
         {
           bg07:{
             width:764,
             height:1800,
             position: { x: 0, y: -800 }
           }
        },
         {
           bg08:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           }
        },
         {
           bg09:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           }
        },
         {
           bg10:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           }
        },
         {
           bg11:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           }
        },
         {
           bg12:{
             width:764,
             height:1800,
             position: { x: 0, y: 0 }
           }
        }
      ],
      sprites:{},//精灵集合
      // 精灵动画集合
      animationsOptions:{
        bg01Womam:[
          {
            delay:0,
            duration: 0.28,
            to: { x:-200, y:1400}
          }
        ],
        bg03Postman:[
          {
            delay:0.15,
            duration: 0.2,
            to: { x:400, y:980}
          }
        ],
        bg04Professionalwomen:[
          {
            delay:0.18,
            duration: 0.2,
            to: { x:-200, y:500}
          }
        ],
        bg05train:[
          {
            delay:0.2,
            duration: 0.15,
            to: { x:-230, y:40}
          }
        ],
        bg06rail:[
          {
            delay:0.3,
            duration: 0.2,
            to: { x:-200, y:-575}
          }
        ]
      }
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
      let _that =this;
      const w = document.body.clientWidth;
      const  h = document.body.clientHeight; 
    let app = new Application({ 
        width:w,
        height:h,                      
        antialiasing: true, 
        transparent: true, 
        resolution: 1,
        backgroundColor: 0x1d9ce0,
      }
    );
    document.getElementById("longhua").appendChild(app.view);
    //解决画面模糊
    app.renderer.autoDensity=true;
    app.renderer.resize(w,h);
     // 获取屏幕宽高，判断横屏还是竖屏
    let min = (w < h) ? w : h;
    let scale = min / 750;  // 根据设计稿尺寸进行缩放比例调整
    app.stage.scale.set(scale, scale);  // 根据屏幕实际宽高放大舞台
    let max = (w > h) ? w : h;
    
    //导入资源
    loader
    .add('bg01',require("../img2/01.jpg"))
    .add("bg01Womam",require("../png/wuman.png"))
    .add('bg02',require("../img2/02.jpg"))
    .add('bg03',require("../img2/03.jpg"))
    .add('bg03Postman',require("../png/Postman.png"))
    .add('bg04',require("../img2/04.jpg"))
    .add('bg04Professionalwomen',require("../png/Professionalwomen.png"))
    .add('bg05',require("../img2/05.jpg"))
    .add("bg05train",require("../png/train.png"))
    .add('bg06',require("../img2/06.jpg"))
    .add("bg06rail",require("../png/rail.png"))
    .add('bg07',require("../img2/07.jpg"))
    .add('bg08',require("../img2/08.jpg"))
    .add('bg09',require("../img2/09.jpg"))
    .add('bg10',require("../img2/10.jpg"))
    .add('bg11',require("../img2/11.jpg"))
    .add('bg12',require("../img2/12.jpg"))
    .load(setup)
    //进度加载
    loader.onProgress.add((target)=>{
      document.getElementById("loading").innerText = parseInt(target.progress) + "%";
    })
    //加载完成
    loader.onComplete.add((target)=>{
      document.getElementById('loading').style.display = 'none';
      _that.initAnimation();
      app.stage.h = h;
      let scrollDis = app.stage.height - max;
      //滚动初始化
      new AlloyTouch({
            touch: "body", // 反馈触摸的dom
            vertical:true, // 不必需，默认是true代表监听竖直方向touch
            min:-scrollDis, // 不必需,运动属性的最小值
            maxSpeed: 1,
            max: 0, // 不必需,滚动属性的最大值
            bindSelf: false,
            initialValue: 0,
            change: function (value) {
              console.log(value)
              if(value){
                app.stage.position['y'] = value;
                let progress = -value / scrollDis;
                progress = progress < 0 ? 0 : progress;
                progress = progress > 1 ? 1 : progress;
                timeline.seek(progress);
              }
              
            }
          })
         
    })
    //设置画面
    function setup(){
          //初始化场景
           _that.scenesOptions.forEach((item,index)=>{
                let scene ={};
                 scene.name = new Container({
                    width:item.width,
                    height:item.height
                 });
               scene.name.y=item.y;
              _that.scenesList.push(scene);
              app.stage.addChild(scene.name);
           })
           console.log('scenesList',_that.scenesList)
           //初始化精灵
           _that.spritesOptions.forEach((item,index)=>{
             let obj = item;
             //遍历一个场景中的
              for (let key in obj) {
                if (obj.hasOwnProperty(key)) {
                  _that.sprites[key] = PIXI.Sprite.fromImage(key);
                  initSprite(_that.sprites[key], obj[key],index);
                }
              }
           })
           function initSprite(sprite, prop,index) {  // 初始化单个精灵的属性并加入对应的场景中
              for (let key in prop) {
                if (prop.hasOwnProperty(key)) {
                  sprite[key] = prop[key];
                }
              }
              _that.scenesList[index].name.addChild(sprite);
            }
         }
    },
    //初始化运动
    initAnimation(){
        for (let key in this.animationsOptions) {
          if(this.animationsOptions.hasOwnProperty(key)){
            let obj = this.animationsOptions[key];
            obj.forEach((item,index)=>{
                let target = this.sprites[key];
                let act =  TweenMax.to(target,item.duration,item.to);
                let tm = new TimelineMax({ delay:item.delay});
                tm.add(act, 0);
                tm.play();
                timeline.add(tm, 0);
            })
          }
        }
       
    }
  },
};
</script>