<template>

    <MonthsList v-on:SelectedMonth="updateSelectedMonth"></MonthsList>
    <p>Mês selecionado: {{ monthSelected }}</p>

    <table @click="DataObject()" ref="calendar">
        <thead>

            <tr>
                <td>
                <th>Dom</th>
                </td>
                <td>
                <th>Seg</th>
                </td>
                <td>
                <th>Ter</th>
                </td>
                <td>
                <th>Quar</th>
                </td>
                <td>
                <th>Quin</th>
                </td>
                <td>
                <th>Sex</th>
                </td>
                <td>
                <th>Sáb</th>
                </td>
            </tr>
        </thead>
        <tbody ref="weeks">
        
        </tbody>
    </table>

</template>
<script>
import MonthsList from './MonthsList.vue';


export default {
    name: 'Calendar',
    components: {
        MonthsList
    },
    data() {
        return {
        
            monthSelected: "",
            dateObj: new Date(new Date().getFullYear(), new Date().getMonth(), 1),
            monthsName: ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho', 'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'],
        }
    },   
    methods: {


        updateSelectedMonth(month, index) {
            this.monthSelected = month;
            this.SetDaysOfMonth(index);
        },
        SetDaysOfMonth(index) {
            let date = new Date(new Date().getFullYear(), index);
            let currentMonth = date.getMonth(); // baseado em 0 
            const daysInMonth = new Date(date.getFullYear(), currentMonth + index, 0).getDate();
            let weekDays = Math.ceil(daysInMonth / 7)
            let monthBegin = new Date(date.getFullYear(), currentMonth + index, 1).getDay();
            this.GenerateCalendar(weekDays, monthBegin, daysInMonth)
        
        },
        GenerateCalendar(weekDays, monthBegin, daysInMonth) {
            this.$refs.weeks.innerHTML = '';
            let acm = 0;

            // Semanas 
            for (let i = 0; i <= weekDays; i++) {
                let tr = document.createElement("tr");
              
                // Distribuindo os dias em cada semana
                for (let j = 0; j < 7; j++) {
                    let td = document.createElement('td');
                    if (acm > daysInMonth) {
                        break;
                    }
                    if (i === 0 && j < monthBegin) {
                        td.textContent = '';
                    
                    } else if (i === 0 && j === monthBegin) {
                        // primeiro dia do mês
                        acm = 1;
                        td.textContent = acm;


                    }else if(acm <= daysInMonth){
                        td.textContent = acm;
                    }
                    acm++;
                  
                    tr.appendChild(td);
                    this.$refs.weeks.appendChild(tr);



                }
                    
            }
        
        },

    },



}




</script>