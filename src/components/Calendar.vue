<template>
    <div class="m-auto my-5" style="width:400px; height: 290px;">
        <h1 class="text-2xl my-2 text-center" >
            Calendário Vue
        </h1>
        
            <h1 class="my-5">
                Hoje:  {{day_month}} de {{actual_month()}} de {{actual_year}}
            </h1>
        <section class="mx-2">

       <h2 class="font-bold">
 {{month()}} de {{year}}
       </h2> 
        </section>

<section class="flex my-2 " >
            <p class="text-center" style="width: 14.28%" 
            v-for="(day, index) in days_week" :key="index" >
            {{day}}
            </p>
            </section>
            <section class="flex flex-wrap">
                <p :style="{width: '14.28%'}" 
                v-for="number in first_day_of_month()" :key="number">
                    
                </p>
            <p :style="{fontWeight: new Date(year, month_number, 
            days).toDateString()===new Date().toDateString()?  'bold':'' , width: '14.28%' }" 
            class=" text-center" style="width: 14.28%" 
            v-for="days in last_day_of_month()" :key="days">
            {{days}}

            </p>
        </section>
            </div>
<div class="m-auto " style="width:400px; ">

        <section class="flex justify-between my-6" >
                <button @click="prev" class="px-2 rounded border">
                    Prev
                </button>

    <button @click="next" class="px-2 rounded border">
        Next
    </button>
</section>
</div>

</template>


<script>

export default {



  
    
    methods:{

        actual_month(){
            let mes = new Date().toLocaleString('default', {month: 'long'})
            mes = mes.charAt(0).toUpperCase() + mes.slice(1)
            return mes
        }
        ,


prev(){
 this.month_number --;
            if(this.month_number <0){
                this.month_number = 11;
                this.year --;
            }
},
        next(){
            this.month_number ++;
            if(this.month_number > 11){
                this.month_number = 0;
                this.year ++;
            }
        },

        last_day_of_month(){
                    return new Date(this.year, this.month_number+1, 0).getDate();
        },
        first_day_of_month(){
                    return new Date(this.year, this.month_number , 1).getDay();
        },
month(){
let mes =   new Date(this.year, this.month_number).toLocaleString('default', {month: 'long'})
 mes = mes.charAt(0).toUpperCase() + mes.slice(1)
            return mes 
}
    
    },
    data(){
       

            return {
            
 day_month:  new Date().getDate(),

actual_year: new Date().getFullYear(),


month_number:new Date().getMonth() ,


year: new Date().getFullYear(),

           days_week: ['Sun', 'Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat']
            
         
        }
    }
}


</script>

<style>
</style>