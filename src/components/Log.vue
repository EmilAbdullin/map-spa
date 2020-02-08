<template>
    <div class='log-item-wrapper'>
        <div class="log-date">{{log.date}}</div>
        <div class="points">{{log.firstPoint}} - {{log.secondPoint}}</div>
        <div class="distance">{{log.distance}}</div>
    </div>
</template>

<script>
export default {
    props:['log']
}
</script>

<style scoped>

.log-item-wrapper{
    display: flex;
    width: 75%;
    justify-content: space-between;
    padding: 15px;
    border: 1px solid #ececec;
    border-radius: 5px;
    box-shadow: 0 0 10px 1px #f6f6f6;
    color: #3C4043;
    font-weight: bold;
    margin:15px auto;
}
@media (max-width: 768px) {
    .log-item-wrapper{
        width:100%;
        padding:15px;
    }
}

</style>