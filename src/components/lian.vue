<template>
  <div id="Linkage">
    <template v-for="(select,index) in level">
      <select @change = "selectChildren(index)" :key="index" v-model="cataValue[index]">
         <option :value="item" v-for="(item,index) in select">{{item.name}}</option>
      </select>
    </template>
    <br/>
  </div>
</template>

<script>
    export default {
        props: {
          lists: {
            type: Array,
            default: () => []
          },
          curId: {
            type: Number,
            default: null
          }
        },
        data: function () {
          return {
            level:[],
            cataValue:[],
            newArr:[]
          }
        },
        computed:{
          root() {
            const rootData = this._getChid(this.lists, 0)
            return rootData
          }
        },
        methods: {
          selectChildren(_index) {
            this.level.splice(_index+1 , this.level.length)
            let childrenData = this._getChid(this.lists, this.cataValue[_index].id)
            if(childrenData.length){
              this.level[_index+1] = childrenData
            }
          },
          _set(id) {
            let cur = this.lists.filter(item => item.id === id)
            this._getPar(cur[0])
          },
          _getChid(lists, id) {
            return lists.filter(item => item.parent_id === id)
          },
          _getPar(item) {
            let t_l = []
            this.level.unshift(this._getChid(this.lists, item.parent_id))
            this.cataValue.unshift(item)
            if(item.parent_id == 0) {
              return
            }
            let next = this.lists.filter(list => list.id === item.parent_id)
            this._getPar(next[0])
          },
          parseData(lists, parent_id = 0, depth = 0) {
            return lists.filter(list => list.parent_id == parent_id).map(item => {
              item.id = item.id
              item.depth = depth
              item.children = this.parseData(lists, item.id, ++depth)
              return item 
            })
          }
        },
        mounted(){
          if(this.curId){
            this._set(this.curId)
          }else{
            this.level.push(this.root)
          }
        }
    }
</script>

<style scoped>
  #Linkage{height:50px;}
</style>
