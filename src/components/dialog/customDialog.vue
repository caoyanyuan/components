<template>
    <el-dialog :visible.sync="isShowMe"
                :title="title"
                :width="_width"
                :top="top"
                class="custom-dialog"
                :close-on-click-modal="isClosedByParent"
                :class="{'no-title-line': isShowTitleLine}">
        <slot></slot>

        <div slot="title" v-if="titleTabs.length">
            <table-tab class="mt30" :tabs='titleTabs' v-model="activeIndexTable" @tabClick="tabClick"></table-tab>
        </div>
        <div slot="title" v-if="hideTitle">
        </div>
        <el-tabs slot="title" v-if="titleList.length" v-model="activeIndexTable" type="card" class="title-wrap">
            <el-tab-pane
                v-for="(item,index) in titleList"
                :key="index"
                :name="`${index}`"
                :label=item
                >
            </el-tab-pane>
        </el-tabs>
    </el-dialog>
</template>

<script>
import TableTab from 'base/tab/tableTab'

export default {
    props: {
        isShow: {
            required: true,
            type: Boolean,
        },
        title: {
            type: String,
        },
        isShowTitleLine: {
            type: Boolean,
            defualt: true
        },
        width: {
            default: "50%"
        },
        titleTabs: {
            default: () => []
        },
        titleList: {
            default: () => []
        },
        activeIndex: {},
        hideTitle: {},
        isClosedByParent: {
            type: Boolean,
            default: false
        },
        top: {
            default: '15vh'
        }
    },
    data() {
        return {
            isShowMe: false,
            activeIndexTable: 0
        }
    },
    methods: {
        tabClick({oldIndex, newIndex}) {
            this.$emit('tabClick', {oldIndex, newIndex})
        }
    },
    computed: {
        _width() {
            let width = "50%"
            if(this.width.indexOf('%') > -1 || this.width.indexOf('px') > -1) {
                width = this.width
            }else{
                width = parseInt(this.getCurrentPx(this.width))+'px'
            }

            return width
        }
    },
    watch: {
        isShow: {
            immediate: true,
            handler(val) {
                this.isShowMe = val
            }
        },
        isShowMe(val) {
            if(!val) {
                this.$emit('update:isShow', false)
            }
        },
        activeIndexTable(index) {
            this.$emit('update:activeIndex', index)
        },
        activeIndex(index) {
            if (index !== this.activeIndexTable) {
                this.activeIndexTable = `${index}`
            }
        }
    },
    components: {
        TableTab
    }
}
</script>

<style lang="less" scoped>

@h14: .px2vh(14)[@result];
@h16: .px2vh(16)[@result];
@h60: .px2vh(60)[@result];

@import "~@less/element/dialog";

.custom-dialog{
    /deep/ .tabs .tab-item.active{
        background: #072045;
        border-bottom:1px solid #072045;
    }
    /deep/ .el-table .el-table__header-wrapper table{
        background: #072045
    }
}

.title-wrap{
    padding-right: 40px;margin-top: @h20;
    /deep/ .el-tabs__header{
        border-color: @border6;
        .el-tabs__nav {
            border: 0px none;
        }
        .el-tabs__item{
            color:#fff; border:0px none;
            &.is-active, &:hover{
                color: @th-border; border: 1px solid @border6;border-bottom: 0px none;
            }
        }
    }

}
</style>
