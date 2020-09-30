<!--
 * @Author: your name
 * @Date: 2020-09-30 16:10:24
 * @LastEditTime: 2020-09-30 17:33:39
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \pixi\src\page\index.vue
-->
<template>
  <div></div>
</template>
<script>
export default {
  data() {
    return {};
  },
  created() {
    // this.initPixi();
  },
  methods: {
    /**
     * @describe: 初始化数据
     * @param {type}
     * @return {type}
     */
    initPixi() {
      let app = new PIXI.Application({ 
        width: 256, 
        height: 256,                       
        antialiasing: true, 
        transparent: false, 
        resolution: 1
    }
    );

//Add the canvas that Pixi automatically created for you to the HTML document
      document.body.appendChild(app.view);
      document.body.appendChild(app.view);
      PIXI.loader
        .add("../images/cat.png")
        .load(setup);
            //This `setup` function will run when the image has loaded
                function setup() {

                //Create the cat sprite
                let cat = new PIXI.Sprite(PIXI.loader.resources["../images/cat.png"].texture);
                
                //You can also create the `cat` sprite from the texture, like this:
                //let cat = new PIXI.Sprite(PIXI.TextureCache["images/cat.png"]);

                //Add the cat to the stage
                app.stage.addChild(cat);

                //If you ever need to, here's how you can clean out WebGL's GPU
                //memory manually
                /*
                Object.keys(TextureCache).forEach(function(texture) {
                    TextureCache[texture].destroy(true);
                });
                */
            }
    },
    inint() {},
  },
};
</script>