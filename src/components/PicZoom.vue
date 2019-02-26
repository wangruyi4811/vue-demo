<template>
    <div class="pic-box"> <!--pic-box:width:500px;height:500px-->
        <pic-zoom url="https://cdn.bestseller.com.cn/goodsImagePC/JACKJONES/218314526/218314526E39/7201280/218314526E39_p1.jpg" :scale=3 big-url="https://cdn.bestseller.com.cn/goodsImagePC/JACKJONES/218314526/218314526E39/218314526E39_p1.jpg"></pic-zoom>
    </div>
    
</template>
<script>
import PicZoom from 'vue-piczoom'
export default {
  name: 'Piczoom',
  components: {
    PicZoom
  }
}
</script>
<style>
.pic-box {
 width: 500px;
 height: 500px;
}

</style>
