<!--
 * @Author: your name
 * @Date: 2020-09-30 16:10:24
 * @LastEditTime: 2020-10-07 23:01:02
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \pixi\src\page\index.vue
-->
<template>
  <div class="loading" id="loading">加载中0%</div>
</template>
<script>
import * as PIXI from 'pixi.js'
let Application = PIXI.Application,
    Container = PIXI.Container,
    loader = PIXI.loader,
    resources = PIXI.loader.resources,
    TextureCache = PIXI.utils.TextureCache,
    Sprite = PIXI.Sprite;
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
    let app = new Application({ 
        width:w,
        height:800,                      
        antialiasing: true, 
        transparent: false, 
        resolution: 1,
        backgroundColor: 0x1d9ce0,
      }
    );
    document.body.appendChild(app.view);
    //导入资源
    loader.add('bed_boy',require("../imgs/bed_boy.png"))
    .add('bed',require("../imgs/bed.png"))
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
    function setup(){
            let boy = new Sprite(resources['bed_boy'].texture);
            boy.anchor.set(0.5);//设定中心锚点为中间
            boy.x = app.screen.width/2;//将位置设置为中间
            boy.y = app.screen.height/2;
           // app.stage.addChild(tow);//将精灵贴图放进舞台中
            let boyContainer = new Container();
            boyContainer.addChild(boy);
            app.stage.addChild(boyContainer);
            boyContainer.position.set(0,0);
            app.ticker.add(() => {
              // 每秒调用该方法60次(60帧动画)
              boy.rotation += 0.06;
            })
         }
    }
  },
};
</script>