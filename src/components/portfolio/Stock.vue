<template>
    <div class="col-md-4">
        <div class="panel panel-info">
            <div class="panel-heading">
                <h3 class="panel-title">
                    {{stock.name}}
                    <small>價格：{{stock.price}} | 數量：{{stock.quantity}}</small>
                </h3>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input :class="{danger : insufficientQuantity}" type="number" class="form-control" placeholder="數量" v-model="quantity">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" @click="sellStock" :disabled="insufficientQuantity || quantity <=0 || !Number.isInteger(parseInt(quantity))">{{insufficientQuantity ? '數量不足' : '賣出'}}</button>
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
import {mapActions} from 'vuex';
    export default{
        props:['stock'],
        data(){
            return {
                quantity:0
            }
        },
        computed:{
            insufficientQuantity(){
                return this.quantity > this.stock.quantity;
            }
        },
        methods:{
            ...mapActions({
                sellOwnStock:'sellStock'
            }),
            sellStock(){
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    quantity: this.quantity
                };
                this.sellOwnStock(order);
                this.quantity = 0;
            }
        }
    }
</script>
