<template>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <router-link to="/" class="navbar-brand">股票</router-link>

        <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <ul class="navbar-nav mr-auto">
                <router-link to="/portfolio" activeClass="active" tag="li" class="nav-item"><a class="nav-link">Portfolio</a></router-link>
                <router-link to="/stocks" activeClass="active" tag="li" class="nav-item"><a class="nav-link">Stocks</a></router-link>
            </ul>
            <strong class="navbar-text navbar-auto">基金:{{funds | currency}}</strong>
            
            <ul class="navbar-nav navbar-right">
                <a href="#" class="navbar-text navbar-auto" @click="endDay">結束今日交易</a>
                
            </ul>
        </div>
    </nav>
</template>

<script>
    import {mapActions} from 'vuex';

    export default{
        data(){
            return{
                
            }
        },
        computed:{
            funds(){
                return this.$store.getters.funds;
            }
        },
        methods:{
            ...mapActions([
                'randomizeStocks'
            ]),
            endDay() {
                this.randomizeStocks();
            }
        }
    }
</script>