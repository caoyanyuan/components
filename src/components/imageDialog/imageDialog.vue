
<template>
    <custom-dialog :is-show.sync="visibile" width="1000">
        <div class="scale-container">
            <div class="thumb fl">
                <img-icon class="arrow-top ilt" @onClick="onPrev"  type='arrow-top' :w=40 :h=40 m="0 0 10 0"></img-icon>
                <div class="listcon" ref=thumbWrap>
                    <ul ref="thumbList">
                        <li v-for="(item, i) in images" :key="i"
                            :class="{active:i==currentIndex}" 
                            @click="currentIndex=i">
                            <img-box :url=item.src :w=120 :h=height />
                        </li>
                    </ul>
                </div>

                <img-icon class="arrow-down ilt" @onClick="onNext" type='arrow-down' :w=40 :h=40></img-icon>
            </div>
            <div class="large fl" ref="large">
                <video :src="images[currentIndex].src" width=100% height=100% autoplay="autoplay" loop="loop" preload="true" muted ref="video"></video>
            </div>
            <div class="clear"></div>
        </div>
    </custom-dialog>
</template>

<script>
//基础element UI custom dialog 
import CustomDialog from "./customDialog"

const IMAGE_HEIGHT = 100
const NUM = 5
const MARGIN = 10

export default {
    props: {},
    data() {
        return {
            visibile: true,
            images: [
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
                { src: 'static/img/manage/dynamic.png', text: 'xxx' },
            ],
            currentIndex: 0,
            top: 0
        }
    },
    methods: {
        onPrev() {
             if(this.top==0) {
                return 
            }else{
                this.top = this.top - this.heightPX
            }
        },
        onNext(type) {
            if(this.top==this.maxTop) {
                return 
            }else if(this.top < this.maxTop){
                this.top = this.top + this.heightPX
            }
        }
    },
    watch: {
        top(value) {
            let min = parseInt(value / this.heightPX)
            
            this.currentIndex = Math.max(this.currentIndex, min)
            this.currentIndex = Math.min(this.currentIndex, min + NUM - 1)
            
            this.$refs.thumbList.style.marginTop = -value + 'px'
        }
    },
    mounted() {
        let hei =  this.heightPX * NUM 
        this.$nextTick(() => {
            this.$refs.thumbWrap.style.height = hei + 'px'
            this.$refs.large.style.height = hei - this.marginPX + 'px'
        })
    },
    created() {
        this.height = IMAGE_HEIGHT
        this.marginPX = parseInt(this.getCurrentPx(MARGIN))
        this.heightPX = parseInt(this.getCurrentPx(IMAGE_HEIGHT + MARGIN))
        this.maxTop = (this.images.length - NUM) * this.heightPX
    },
    components: {
        CustomDialog
    },
}
</script>

<style lang="less" scoped>
@w120: .px2vw(120)[];
@w780: .px2vw(780)[];

.scale-container{
    padding:0 @w40;
    .thumb{
        width: @w120;margin-right:20px;text-align:center;
        .listcon{
            height:@w780;overflow:hidden;
            ul {
                transition:margin ease .3s;
                li {
                    margin-bottom: @w10;
                    &.active{
                        /deep/ .image-box{
                            border:2px solid @border;
                        } 
                    }
                }
            }
        }
    }
    .large{
        margin-top:@w50; width: 32vw;
        video{
            width: 100%;
        }
    }
}
</style>
