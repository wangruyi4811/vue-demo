<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png">
    <Layer title="最基本示例" v-model="showLayer" content="21231313" confirm="确定" cancel="取消" :showClose="showClose" :autoClose="autoClose"/>
    <p @click="showLayer=true">{{}}</p>
  
    <p>{{ a }}</p>
    <Will msg="Welcome to Your Vue.js App"/> -->
    <Magnifier 

    />
    <!-- <Modal title="123123213213"	visible="" /> -->
    <!-- <Button type="primary" block="showLayer"/> -->
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue';
import Will from './components/Will.vue';
import Magnifier from './components/Magnifier.vue';
import Layer from './components/Layer.vue';
import { Modal } from "ant-design-vue/es";
import { Button } from "ant-design-vue/es";
export default {
  name: 'app',
  data: function(){
    return {
      showClose: true,
      showLayer: false,
      autoClose: 2,
      a: 1,
      urlArr: [
        {url: 'https://www.baidu.com', name:'baidu'},
        {url: 'https://www.sina.com',name: 'sina'}
      ],
      configs: {
             width:650,
             height:350,
             maskWidth:100,
             maskHeight:100,
             maskColor:'red',
             maskOpacity:0.2
           }
    }
  },
  created: function(){
    console.log('created');
    console.log('a is: ' + this.a);
  },
  mounted: function(){
    console.log('mounted');
    console.log('a is: ' + this.a);
    this.a = 2;
    //document.getElementsByTagName('title')[0].innerHTML = '新的title';
    console.log(document.getElementsByTagName('title')[0].innerHTML);


    if (window.DeviceMotionEvent) {
        window.addEventListener('devicemotion',deviceMotionHandler,false);
    }
 
    //获取加速度信息
    //通过监听上一步获取到的x, y, z 值在一定时间范围内的变化率，进行设备是否有进行晃动的判断。
    //而为了防止正常移动的误判，需要给该变化率设置一个合适的临界值。
    var SHAKE_THRESHOLD = 4000;
    var last_update = 0;
    var x, y, z, last_x = 0, last_y = 0, last_z = 0;
    function deviceMotionHandler(eventData) {
            var acceleration =eventData.accelerationIncludingGravity;
            var curTime = new Date().getTime();
            if ((curTime-last_update)> 10) {
                var diffTime = curTime -last_update;
                last_update = curTime;
                x = acceleration.x;
                y = acceleration.y;
                z = acceleration.z;
                var speed = Math.abs(x +y + z - last_x - last_y - last_z) / diffTime * 10000;
                if (speed > SHAKE_THRESHOLD) {
                    alert("你中奖啦！");  // Do something
                }
                last_x = x;
                last_y = y;            
                last_z = z;
            }
    }
  },
  updated: function(){
    console.log('updated');
    console.log('a is: ' + this.a);
  },
  methods: {
    openLayer(){
        //this.showLayer = true;
     },
  },
  components: {
    Will,
    Magnifier,
    Layer,
    Modal,
    Button
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
html {
  /* font-size: 0; */
}
img{
  border: 0;
  display:block;
}
</style>
