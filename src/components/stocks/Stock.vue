<template>
    <div class="col-md-4">
        <div class="panel panel-success">
            <div class="panel-heading">
                <h3 class="panel-title">
                    {{stock.name}}
                    <small>價格：{{stock.price}}</small>
                </h3>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input :class="{danger : insufficientFunds}" type="number" class="form-control" placeholder="數量" v-model="quantity">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" @click="buyStock" :disabled="insufficientFunds || quantity <=0 || !Number.isInteger(parseInt(quantity))">{{insufficientFunds ? '餘額不足' : '購買'}}</button>
                </div>
            </div>
        </div>
    </div>  
</template>

<style scoped>
    .danger {
        border:1px solid red;
    }
</style>

<script>
    export default{
        props:['stock'],
        data(){
            return {
                quantity:0
            }
        },
        computed:{
            funds(){
                return this.$store.getters.funds;
            },
            insufficientFunds(){
                return this.quantity * this.stock.price > this.funds;
            }
        },
        methods:{
            buyStock(){
                const order = {
                    stockID : this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                }
                this.$store.dispatch('buyStocks',order);
                this.quantity = 0;
            }
        }
    }
</script>
