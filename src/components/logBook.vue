<template>
    <div class="logbook-wrapper">
        <h2 class="subheading">Logs:</h2>
        <Log
        v-for="(log,key) of logs"
        :key="key"
        v-bind:log="log"
        />
    </div>
</template>


<script>
import Log from "@/components/Log"
export default {
    props:['logs'],
    components:{
        Log
    }
}
</script>


<style scoped>

.logbook-wrapper{
    max-width: 768px;
    margin: 0 auto;
}
.subheading{
    font-size:1.5em;
    text-align: center;
    color: #3C4043;
}

</style>



