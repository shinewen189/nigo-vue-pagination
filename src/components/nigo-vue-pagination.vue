<template>
    <div class="_page_container">
        <ul class="_pages _pages_1">
            <li :class="['_home', setFristDisabled]" @click.prevent="setHomePageination">首页</li>
            <li :class="['_prev_ _prev' ,setFristDisabled]" @click="prevPageination">上一页</li>
            <li :class="['_pages_li_1',getCurrent(item)?'_active_1':'']"
                :style="{backgroundColor : getCurrent(item) ? color : ''}"
                :data-index="item"
                v-for="(item) in pageSizeNum"
                :key="item"
                @click.prevent="switchPageination(item)"
            >{{item}}
            </li>
            <li :class="['_next_ _next', setLastDisabled]"
                @click.prevent="nextPageination">下一页
            </li>
            <li :class="['_last', setLastDisabled]"
                @click="setLastPageination">尾页
            </li>
        </ul>
        <div class="_jumper">
            <span class="_count">共 {{pageTotalNum}} 页</span>
            <span>前往</span>
            <label>
                <input class="_jumper_input"
                       type="number"
                       min="1"
                       :max="pageTotalNum"
                       @blur="jumpPageination($event)"
                       @keyup.enter="jumpPageination($event)"/>
            </label>
            <span>页</span>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'pagination',
        props: {
            // 总数据
            pageTotal: {
                type: Number,
                default: 100
            },
            // 分页大小
            pageSize: {
                type: Number,
                default: 10
            },
            //显示页数
            pageNum: {
                type: Number,
                default: 5
            },
            //自定义颜色
            color: {
                type: String,
                default: '#409eff'
            }
        },
        data() {
            return {
                current: 1,
                pageSizeNum: Array.from({length: this.pageNum}, (_, index) => index + 1),
                pageTotalNum: Math.ceil(this.pageTotal / this.pageSize)
            }
        },
        computed: {
            getCurrent() {
                return (index) => {
                    return this.current === index
                }
            },
            setFristDisabled() {
                return this.current === 1 ? '_disabled_c _disabled' : ''
            },
            setLastDisabled() {
                return this.current === this.pageTotalNum ? '_disabled_c _disabled' : ''
            }
        },
        watch: {
            current(newVal) {
                let temp = [],
                    max,
                    min = newVal - Math.floor(this.pageNum / 2)
                if (min < 1) min = 1
                max = min + this.pageNum - 1
                if (max > this.pageTotalNum) max = this.pageTotalNum
                for (let i = min; i <= max; i++) {
                    temp.push(i)
                }
                this.pageSizeNum = temp
            }
        },
        updated() {
            this.$emit('currentCallBack', this.current - 1)
        },
        methods: {
            switchPageination(index) {
                this.current = index
            },
            nextPageination() {
                if (this.current === this.pageTotalNum) {
                    this.current = this.pageTotalNum
                }else {
                    this.current++
                }
            },
            prevPageination() {
                if (this.current === 1) {
                    this.current = 1
                }else {
                    this.current--
                }
            },
            setHomePageination() {
                this.current = 1
            },
            setLastPageination() {
                this.current = this.pageTotalNum
            },
            jumpPageination(ev) {
                let value = Number(ev.currentTarget.value)
                if (value < 1) value = 1
                if (value > this.pageTotalNum) value = this.pageTotalNum
                this.current = value
            }
        }
    }
</script>

<style scoped>


    ._page_container {
        height: 28px;
        line-height: 28px;
        text-align: center;
        user-select: none;

    }

    ._page_container input[type=number] {
        -moz-appearance: textfield;
    }

    ._page_container input[type=number]::-webkit-inner-spin-button,
    ._page_container input[type=number]::-webkit-outer-spin-button {
        -webkit-appearance: none;
        margin: 0;
    }

    ._page_container ._pages {
        display: inline-block;
    }

    ._page_container ._pages li {
        display: inline-block;
        list-style: none;
        vertical-align: top;
        color: #303133;
        font-weight: bold;
        min-width: 30px;
        text-align: center;
        margin: 0 5px;
        border-radius: 2px;
        cursor: pointer;
    }

    ._page_container ._pages li:hover {
        opacity: .6;
        transition-duration: 500ms;
        transition-timing-function: ease;
    }

    ._page_container ._pages li:first-child, ._page_container ._pages li:last-child {
        font-size: 14px;
    }

    ._page_container ._pages ._prev, ._page_container ._pages ._next, ._page_container ._pages ._home, ._page_container ._pages ._last {
        font-size: 12px;
        font-weight: normal;
        padding: 0 8px;
    }

    ._page_container ._jumper {
        display: inline-block;
        color: #606266;
        margin-left: 10px;
    }

    ._page_container ._jumper ._count {
        margin-right: 10px;
    }

    ._page_container ._jumper ._jumper_input {
        display: inline-block;
        font-size: 14px;
        color: #606266;
        width: 50px;
        height: 26px;
        text-align: center;
        margin: 0 5px;
        padding: 3px;
        border: 1px solid #dcdfe6;
        border-radius: 4px;
        background: none;
        outline: none;
        box-sizing: border-box;
    }

    ._page_container ._jumper ._jumper_input:focus {
        border-color: #409eff;
        transition-duration: 500ms;
        transition-timing-function: ease;
    }

    ._pages_1 li {
        background-color: #f4f4f5;
    }

    ._active_1 {
        color: #fff !important;
        transition-duration: 500ms;
        transition-timing-function: ease;
    }

    ._active_2 {
        color: #409eff !important;
    }

    ._disabled {
        cursor: not-allowed !important;
    }

    ._disabled_c {
        color: #c0c4cc !important;
    }

</style>
