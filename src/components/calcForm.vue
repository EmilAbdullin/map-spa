<template>
    <div class="action-form">
        <form @submit.prevent>
            <input type="text" v-model="firstInputVal" :placeholder="form.firstPlaceholder" name="">
            <input type="text" v-model="secondInputVal" :placeholder="form.secondPlaceholder" name="">
            <button type="submit" :class="{disabled:isDisabled}" @click="submitForm" v-bind:disabled="isDisabled" >Calc</button>
            <button class="clear-inputs" :class="{disabled:isDisabled}" @click="clearInput" v-bind:disabled="isDisabled">Clear</button>
        </form>
    </div>
</template>

<script>

export default{
    props:['form'],
    data(){
        return{
            firstInputVal:'',
            secondInputVal:'',
            isDisabled:false
        }
    },
    methods:{
        clearInput(){
            this.firstInputVal = '';
            this.secondInputVal = '';
        },
        submitForm(){
            if(this.firstInputVal !=='' && this.secondInputVal !== ''){
                this.isDisabled = true;
                this.getDistance(this.firstInputVal.trim(),this.secondInputVal.trim());
                this.firstInputVal = '';
                this.secondInputVal = '';
            }else{
                alert('Есть незаполненные поля');
            }
        },
        getDistance(firstPoint,secondPoint){
            ymaps.geocode(firstPoint, {
                results: 1
            }).then(res => {
                let firstCoords = res.geoObjects.get(0).geometry.getCoordinates();
                ymaps.geocode(secondPoint,{
                    results:1
                }).then(res =>{
                    let secondCoords = res.geoObjects.get(0).geometry.getCoordinates();
                    this.isDisabled = false;
                    let distance = Math.round(ymaps.coordSystem.geo.getDistance(firstCoords,secondCoords)/1000) + ' км';
                    let dateNow = new Date();
                    let hours = dateNow.getHours();
                    let minutes = dateNow.getMinutes();
                    let month = new String(dateNow.getMonth() + 1).length === 1 ? '0' + new String(dateNow.getMonth() + 1) : new String(dateNow.getMonth() + 1);
                    let day = new String(dateNow.getDate()).length === 1 ? '0' + new String(dateNow.getDate()) : new String(dateNow.getDate());
                    let date = month + '/' + day + ' в ' + hours + ':' + minutes;
                    const log = {
                        date,
                        firstPoint,
                        secondPoint,
                        distance
                    } 
                    this.addLog(log);
                    this.clearInput();
                }).catch(err =>{
                    alert('Возможно вы ввели неправильные данные!Попробуйте еще раз')
                    this.clearInput();
                    this.isDisabled = false;
                })
            }).catch(err =>{
                alert('Возможно вы ввели неправильные данные!Попробуйте еще раз')
                this.isDisabled = false;
                this.clearInput();
            })
        },
        addLog(log){
            this.$emit('addnewlog',log);
        }
    }
}
</script>


<style scoped>

.action-form{
    padding:15px;
    width:100%;
}

.action-form form{
    width:100%;
    display: flex;
    justify-content: space-around;
    padding:0 15px;
}

.action-form form button{
    width:100px;
    text-transform: uppercase;
    border-radius: 5px;
    background: none;
    outline:none;
    border:2px solid;
    cursor: pointer;
    font-weight: bold;
}

.action-form form button.clear-inputs{
    border-color: tomato;
    color:tomato;
}

.action-form form button[type="submit"]{
    border-color: #0075B7;
    color:#0075B7;
}

.action-form form input{
   height:30px;
   padding:0 15px;
   border:none;
   border-bottom: 1px solid #ccc;
   outline:none;
   color:#3C4043;
   text-transform: uppercase;
}

.disabled{
    opacity:.25;
}

@media (max-width: 768px) {
    .action-form form{
        width:100%;
        display: flex;
        justify-content: space-around;
        padding:0 15px;
        flex-direction: column;
    }
    .action-form input{
        width:100%;
        margin-bottom:25px;
    }
    .action-form form button{
        width:320px;
        margin:10px auto;
        padding:12.5px;
    }
}

</style>