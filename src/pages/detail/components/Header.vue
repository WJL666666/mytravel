<template>
    <div>
        <router-link  tag="div" to="/" class="header-abs" v-show="showAbs">
            <div class="iconfont header-abs-back">&#xe624;</div>
        </router-link>
        <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
            <router-link to="/">
                <div class="iconfont header-fixed-back">&#xe624;</div>
            </router-link>
             景点详情
        </div>
    </div>
</template> 

<script>

export default {
    name: 'DetailHeader',
    data () {
        return {
            showAbs: true,
            opacityStyle: {
                opacity: 0
            }
        }
    },
    methods: {
        handleScroll () {
            const top = document.documentElement.scrollTop
            if (top>60 && top<140) {
                const opacity = top / 140
                this.opacityStyle = {opacity}
                this.showAbs = false
            } else {
                this.showAbs = true
            }
        }
    },
    // activated () {
    //     window.addEventListener('scroll', this.handleScroll)
    // },
    // deactivated () {
    //     window.removeEventListener('scroll', this.handleScroll)
    // }
    // mounted是挂载vue实例后的钩子函数，activated是组件被激活后的钩子函数，
    // mounted的时候 是不保证组件已在document中。也就是说组件还没有被激活，所以activated可以理解为在mounted之后执行。
    // 在定义变量和执行函数的时候需要注意放置的钩子函数位置。
    mounted () {
        window.addEventListener('scroll', this.handleScroll)
    },
    unmounted () {
        window.removeEventListener('scroll', this.handleScroll)
    }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
    .header-abs
        position: absolute 
        left: .2rem
        top: .2rem
        width: .8rem 
        height: .8rem
        line-height : .8rem
        border-radius: .4rem
        text-align : center
        background: rgba(0,0,0, .8)
        .header-abs-back 
           color: #fff 
           font-size: .4rem 
    .header-fixed
        z-index: 2
        position: fixed
        top: 0
        left: 0
        right: 0
        height: $headerHeight
        line-height: $headerHeight
        text-align: center
        color: #fff
        background : $bgColor
        font-size: .32rem
        .header-fixed-back
            position: absolute
            top: 0
            left:0
            width: .64rem
            text-align: center
            font-size: .4rem
            color: #fff
</style>
