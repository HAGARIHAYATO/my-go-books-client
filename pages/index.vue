<template>
    <section>
        <h5 class="title">Welocome To Your Arrival</h5>
        <p class="message">This Site is For Well Book Reader</p>
        <p class="message">{{ message }}</p>
        <div class="button-wrap">
            <button class="button is-primary" @click="enterSite">YES</button> <button class="button is-primary" @click="notEnterSite">NO</button>
        </div>
    </section>
</template>
<script>
export default {
    data () {
        return {
            message: "Do You Use This Site ?"
        }
    },
    methods: {
        enterSite() {
            this.$router.push("/books")
        },
        notEnterSite() {
            this.message = "Thanks See You Again !"
        }
    }
}
</script>
<style scoped>
    .title{
        font-size: 32px;
        font-weight: bold;
    }
    .message{
        font-size: 24px;
        font-weight: bold;
    }
    .button-wrap{
        margin: 5% auto;
    }
</style>