<template>
    <div>
        <SampleComp :sample="sample" />
        <button @click="clickMe">点我</button>
        <img :src="imgPath" />
    </div>
</template>
<script lang="ts">
    import Vue from "vue"
    import {Component} from "vue-property-decorator"
    import SampleComp from "./component/Sample.vue"
    import {Sample} from "./model/Sample"
    @Component({name: "app", components: {SampleComp}})
    export default class App extends Vue{
        sample: Sample = {Count: 0}
        imgPath: string = require("./img/sample.jpg")
        clickMe() {
            this.sample.Count++;
        }

        loadImage(): Promise<void>{
            return new Promise<void>((resolve, reject) => {
                var img = new Image()
                img.src = "http://unknow.com/unknown"
                img.onload = () => {
                    resolve()
                }

                img.onerror = () => {
                    reject()
                }
            })

        }

        async mounted() {
            try{
                await this.loadImage()
            }
            catch(err){
                console.log("load failure")
            }
        }
    }
</script>
<style scoped lang="css">
    .title{
        color: green;
    }
</style>