<template>
    <div>
        <input :type="type" :value="value" @input="inputChange">
    </div>
</template>

<script>
    export default {
        data() {
            return {

            }
        },
        props: {
            type: {
                type: String,
                default: "text"
            },
            value: {
                type: String,
                default: ""
            }
        },
        methods: {
            //输入值改变，通知父组件
            inputChange(e) {
                this.$emit('input',e.target.value);

                //通知父组件FormItem做校验
                this.$parent.$emit('validate');
            }
        }
    }
</script>

<style scoped>
input{
    outline-style: none ;
    border: 1px solid #ccc; 
    border-radius: 3px;
    padding: 10px 10px;
    width: 620px;
    font-size: 24px;
}
input:focus{
    border-color: #66afe9;
    outline: 0;
    -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6);
    box-shadow: inset 0 1px 1px rgba(0,0,0,.075),0 0 8px rgba(102,175,233,.6)
}
.labelMargin{
    margin-right: 10px;
}

</style>