<template>
    <div>
        <slot></slot>
    </div>
</template>

<script>
    export default {
        //provide 返回对象可以跨层级传参给子孙后代
        provide() {
            return {
                form: this //表单实例传递给后代
            }
        },
        props: {
            model: {
                type: Object,
                required: true
            },
            rules: {
                type: Object
            }
        },
        methods: {
            async validate(cb) {
                //遍历需要校验的子组件，即含有prop的子组件
                const child = this.$children.filter(item => item.prop).map(ele => ele.validate());
                const results = await Promise.all(child);
                if(results.some(ele => !ele)) {
                    //校验失败
                    cb(false)
                }else{
                    //校验成功
                    cb(true)
                }
            }
        },
        
    }
</script>

<style lang="scss" scoped>

</style>