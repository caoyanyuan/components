<template>
  <div>
    <div class="list">
      <span>lian.vue:</span>
      <div class="com-wrap">
        <lian :lists="lianData" :curId="lianCurId"></lian>
      </div>
    </div>
    <div class="list">
      <span>progress-mobile.vue:</span>
      <div class="com-wrap">
       <progress-mobile :percent="percent" class="progress"></progress-mobile>
      </div>
    </div>
    <div class="list">
      <span>progress-pc.vue:</span>
      <div class="com-wrap">
        <progress-pc :value="percent" :min="0" max="100"></progress-pc>
      </div>
    </div>
  </div>
</template>

<script>
import Lian from './lian'
import progressMobile from './progress-Mobile.vue'
import ProgressPc from './progress-pc.vue'

let arrData = [
  {id: 1, parent_id: 0, name: '一级'},
  {id: 2, parent_id: 0, name: '一级2'},
  {id: 12, parent_id: 1, name: '二级1'},
  {id: 13, parent_id: 1, name: '二级2'},
  {id: 122, parent_id: 12, name: '三级1'},
  {id: 133, parent_id: 13, name: '三级2'},
  {id: 1335, parent_id: 133, name: '四级1'},
  {id: 1336, parent_id: 133, name: '四级2'}
]

export default {
  components:{
    Lian,progressMobile,ProgressPc
  },
  data () {
    return {
      lianData: arrData,
      lianCurId: 1335,
      percent: 50
    }
  }
}
</script>

<style lang='less' scoped>
  .list{margin-top:20px;
    span{display:inline-block;width:200px;}
    .com-wrap{display:inline-block;margin-left:10px;vertical-align:middle;}
  }
  .progress{width:300px;}
</style>
