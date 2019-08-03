<template>
    <div class="parent">
        <child>
            <div>123</div>
            <div slot="bt" slot-scope="data">
                {{data}}
            </div>
        </child>
    </div>
</template>
<script>
export default {
    name:'parent',
    components:{
        'child':()=>import('./child-no-scope.vue')
    }
}
</script>

