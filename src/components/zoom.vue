<template>
    <div class="pic-box"> <!--pic-box:width:500px;height:500px-->
       <img-zoom src="https://cdn.bestseller.com.cn/goodsImagePC/JACKJONES/218314526/218314526E39/7201280/218314526E39_p1.jpg" width="450" height="250" bigsrc="img-big.jpg" :configs="configs"></img-zoom>
    </div>
    
</template>
<script>
import imgZoom from 'vue2.0-zoom'
export default {
  name: 'Imgzoom',
  components: { imgZoom },
  data: {
  }
}
</script>
<style>
.pic-box {
 width: 500px;
 height: 500px;
}

</style>
