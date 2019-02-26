<template>
    <div class="mag-box" :style="{height: `${this.samllHeight}px` }">
        <div 
        class="origin-box" 
        :style="{width: `${this.samllWidth}px`, height: `${this.samllHeight}px`}" 
        @mouseover="updateXY"
        @mouseout="isHide"
        >
            <img class="origin-img" :style="{width: `${this.samllWidth}px`, height: `${this.samllHeight}px`}" src="https://cdn.bestseller.com.cn/goodsImagePC/SELECTED/418412561/418412561S01/7201280/418412561S01_p2.jpg" @mousemove.stop="updateXY" @mouseover.stop="updateXY"/>
            <i :style="{
                width: `${this.iconWidth}px`, 
                height: `${this.iconHeight}px`,
                top: `${this.styleIcon.top}`,
                left: `${this.styleIcon.left}`,
                marginLeft:  `${this.styleIcon.marginLeft}`,
                marginTop: `${this.styleIcon.marginTop}`,
                display: this.styleIcon.display
                }" 
            @mousemove.stop="updateXY" @mouseover.stop="updateXY" ref="i"></i>
        </div>
        <div class="big-box" :style="{width: `${this.bigBoxWidth}px`, height: `${this.bigBoxHeight}px`}">
            <img ref="bigImg" class="big-img" src="https://cdn.bestseller.com.cn/goodsImagePC/SELECTED/418412561/418412561S01/418412561S01_p2.jpg" :style="styleBigImg"/>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Magnifier',
    props: {
        iconWidth: {
            type: Number,
            default: 212
        },
        iconHeight: {
            type: Number,
            default: 236
        },
        bigBoxWidth: {
            type: Number,
            default: 680
        },
        bigBoxHeight: {
            type: Number,
            default: 738
        },
        samllWidth: {
            type: Number,
            default: 460
        },
        samllHeight: {
            type: Number,
            default: 738
        }
    },
    data: function () {
        return {
            x: 0,
            y: 0,
            styleIcon: {
                top: '0',
                left: '0',
                display: 'none'
            },
            styleBigImg: {
                transform: 'translate(0,0)'
            },
            bigImgOriginSize: {
                width: 0,
                height: 0
            }
        }
    },
    mounted: function(){
       this.bigImgSize()
    },
    updated: function () {
       // updateXY()
    },
    methods:{
        updateXY: function(event){
            this.isShow();
            //小图的光标距离左侧的距离
            let mouseX = 0;
            //小图的光标距离顶部的距离
            let mouseY = 0;
            let icon = {
                w: this.iconWidth || 212,
                h: this.iconHeight || 236
            };
            let samllWidth = this.samllWidth || 460;//小视图的宽
            let samllHeight = this.samllHeight || 738;//小视图的高
            let bigW = this.bigBoxWidth || 680;//大视图的宽
            let bigH = this.bigBoxHeight || 738;//大视图的高 
            if(event.target.tagName === 'I'){
                this.styleIcon.left = parseFloat(event.offsetX) + parseFloat(this.$refs.i.offsetLeft) + 'px';
                this.styleIcon.top = parseFloat(event.offsetY) + parseFloat(this.$refs.i.offsetTop) + 'px';
                this.styleIcon.marginLeft = -(icon.w)/2 + 'px';
                this.styleIcon.marginTop = -(icon.h)/2 + 'px';
                
            }else{
                this.styleIcon.left = parseFloat(event.offsetX)  + 'px';
                this.styleIcon.top = parseFloat(event.offsetY)  + 'px';
                this.styleIcon.marginLeft = -(icon.w)/2 + 'px';
                this.styleIcon.marginTop = -(icon.h)/2 + 'px';
                
            }
            //边界判断
            if(parseFloat(this.styleIcon.left) < (icon.w)/2){
                this.styleIcon.left = (icon.w)/2 + 'px';
                //mouseX = 0;
            }
            if(parseFloat(this.styleIcon.left) > (samllWidth - (icon.w)/2)){
                this.styleIcon.left = samllWidth - (icon.w)/2 + 'px';
                //mouseX = 430;
            }
            if(parseFloat(this.styleIcon.top) < (icon.h)/2){
                this.styleIcon.top = (icon.h)/2 + 'px'
                //mouseY = 0;
            }
            if(parseFloat(this.styleIcon.top) > (samllHeight - (icon.h)/2)){
                this.styleIcon.top = samllHeight - (icon.h)/2 + 'px';
                //mouseY = 220;
            }
            mouseX = parseFloat(this.styleIcon.left) - (icon.w)/2;
            mouseY =  parseFloat(this.styleIcon.top) - (icon.h)/2;
            //计算右边大图的位置
            //大图的尺寸
            let bigWidth = this.bigImgOriginSize.width;
            let bigHeight = this.bigImgOriginSize.height;
          
            let bigImgX = (bigW - bigWidth) * (parseFloat(mouseX)) / (samllWidth - (icon.w));
            let bigImgY = (bigH - bigHeight) * (parseFloat(mouseY)) / (samllHeight - (icon.h));

            this.styleBigImg.transform = `translate(${bigImgX}px,${bigImgY}px)`


        },
        bigImgSize: function() {
            let Img = new Image();
            Img.src = this.$refs.bigImg.src;
            Img.onload = () => {
                this.bigImgOriginSize.width = Img.width;
                this.bigImgOriginSize.height = Img.height;
            }
        },
        isShow: function(){
            this.styleIcon.display = "block";
        },
        isHide: function () {
            this.styleIcon.display = "none";
        }
    }
}
</script>
<style>
.mag-box {
    display: flex;
    overflow: hidden;
}
.mag-box div{
    border: 1px solid red;
}
.origin-img {
    height: auto;
}
.origin-box {
    position: relative;
    
}
.origin-box i {
    position: absolute;
    left: 0;
    top: 0;
    background: blue;
    opacity: 0.3;
    cursor: move;
}
.mag-box .big-box {
    overflow: hidden;
}
</style>
