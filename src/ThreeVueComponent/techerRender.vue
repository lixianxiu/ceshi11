
<template></template>


<script>
export default {
    template: `<daaaa 
    class="demo1 demo2" 
    click="click1" 
    @click.native="click1" 
    :style="{color:'blue'}" 
    id="id1" 
    v-bind="{a:1,b:1} " 
    :aaaa="223">
    <span>222</span>
    </daaaa>`, //模版
     render(h) {
 return h('daaaa', {
            class: {
                    demo1: true,
                    demo2: true,
                    other: false
                    },
            style: {
                    color: 'blue'
                    },
            attrs: {
                    id: 'id1',
                    class: 'demo1 demo2'
                    },
            props: Object.assign({}, this.$attrs, {
                    aaaa: 223
                    }),
            on:{
                click:()=>this.click1()
                },
            nativeOn

            },[h('span')])
        }
}
</script>

<style>
</style>

