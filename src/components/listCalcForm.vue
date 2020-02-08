<template>
    <div class="list-forms">
        <button @click="$emit('addNewForm')" class="add-input-form" title="Click for adding">&#10006;</button>
        <calcForm 
        v-for="(form,key) of currentForms"
        :key="key"
        v-bind:form="form"
        v-on:addnewlog="addNewLog"
        />
    </div>
</template>


<script>
import calcForm from './calcForm'
export default {
    props:['currentForms'],
    components:{
        calcForm
    },
    methods:{
        addNewLog(log){
            this.$emit('addlog',log);
        }
    }
}
</script>



<style scoped>
    .add-input-form{
        background:none;
        border-radius:100%;
        border:2px solid #0DBC79;
        outline:none;
        width:40px;
        height:40px;
        text-align: center;
        line-height:20px;
        font-size:1.25em;
        color:#0DBC79;
        transform: rotateZ(45deg);
        cursor: pointer;
        margin-top:15px;
    }
    .list-forms{
        display:flex;
        margin:0 auto;
        max-width: 768px;
        flex-direction: column;
        align-items: center;
    }

</style>