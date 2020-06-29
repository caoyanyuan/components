<template>
    <custom-dialog :is-show.sync="visible" width="70%" title="视频" top="5%">
        <img-icon   class="arrow-left" 
                    @onClick="onPrev" 
                    :class="{disabled:currIndex==0}"
                    type='arrow-left' 
                    :w=60 :h=60
                    />
        <img-icon   class="arrow-right" 
                    @onClick="onNext" 
                    :class="{disabled:currIndex==listData.length-1}"
                    type='arrow-right' 
                    :w=60 :h=60></img-icon>

         <video :src="listData[currIndex].src" width=100% height=100% autoplay="autoplay" loop="loop" preload="true" muted ref="video"></video>
         <div class="text">{{listData[currIndex].text}}</div>
    </custom-dialog>
</template>

<script>
import CustomDialog from "./customDialog"

export default {
    data() {
        return {
            visible: true,
            currIndex: 0,
            listData: [
                { src: 'static/video/scene1.mp4', text: 'xxx' },
                { src: 'static/video/scene1.mp4', text: 'xxx' },
                { src: 'static/video/scene1.mp4', text: 'xxx' },
                { src: 'static/video/scene1.mp4', text: 'xxx' },
            ]
        }
    },
    methods: {
        onPrev() {
            if(this.currIndex > 0) {
                this.currIndex -- 
            }
        },
        onNext() {
            this.currIndex ++
        }
    },
    components: {
        CustomDialog
    }
}
</script>

<style lang="less" scoped>
video{
    max-width: 90%; margin: 0 auto; display: block; 
}
.arrow-left{
    left: 10px; 
}
.arrow-left, .arrow-right{
    top: 50%; transform: translateY(-50%); position: absolute; cursor:pointer; 
    &.disabled{
        cursor:not-allowed ; opacity: 0.3;
    }
}
.arrow-right{
    right: 10px;
}
.text{
    text-align:center; color: #fff; font-size: 20px; margin-top: 10px;
}
</style>


