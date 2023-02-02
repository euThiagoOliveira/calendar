<template>

    <select @change="changeMonth()" v-model="SelectedMonth" >
    <option v-for="(mes, index)  in monthsName" :key="index"  :data-m="index">{{ mes }}</option>
    </select>

</template>
<script>
import Calendar from './Calendar.vue'
export default{

    Name:'MonthsList',
    components:{
        Calendar
    },
    data() {
        return {
        monthsName : ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'],
        SelectedMonth:'',
    }
    },
    computed:{
        SelectedIndex(){
           return this.monthsName.indexOf(this.SelectedMonth)
        }
    },
 
    methods: {
        changeMonth(){
            this.$emit("SelectedMonth", this.SelectedMonth,this.SelectedIndex);
        },
 
    },
    components:{
        "Calendar": Calendar,

    }
}
</script>