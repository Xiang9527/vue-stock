<template>
    <div>
        <h1>股票交易</h1>
        <p>您的基金{{funds | currency}}</p>
    </div>
</template>

<script>
    export default{
        computed:{
            funds(){
                return this.$store.getters.funds;
            }
        }
    }
</script>