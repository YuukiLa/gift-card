<template>
    <div v-show="visible">
        <div class="envelope animated " :class="classes">
            <div class="triangle-down"></div>
            <img class="heart" :src='iconurl' @click="handleClick"/>
            <div class="triangle-up"></div>
            <div class="text">你收到一封信，点击查收！</div>
        </div>
    </div>
</template>

<script>
    import iconurl from '../assets/爱心.png'
    export default {
        name: "First",
        computed: {
            iconurl: function () {
                return iconurl
            }
        },
        data() {
            return {
                visible: true,
                classes: "bounceInLeft"

            }
        },
        methods: {
            handleClick: function () {
                this.visible = false
                this.classes = 'bounceOutRight'
                this.$emit("show")
            }
        }
    }
</script>

<style>

</style>
