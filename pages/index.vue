<template>
<v-app>
<v-container class="white px-10">

<v-row v-for="(input,index) in inputs" :key="index">

<v-col
cols="12"
md="6"
>
<v-text-field
v-model="input.task"
label="Task"
required
></v-text-field>
</v-col>

<v-col
cols="12"
md="4"
>
<v-text-field
type="number"
v-model="input.duration"
label="Duration"
required
></v-text-field>
</v-col>

<v-col
cols="12"
md="2"
>
<v-icon class="py-4 red--text"   @click="deleteRow(index)">mdi-delete</v-icon>
</v-col>


<v-col
cols="12"
md="2"
>

</v-col>
</v-row>
<v-row>
<v-col
cols="12"
md="2"
>
Total No. of Days {{total}}
</v-col>
</v-row>

<v-row>
<v-col
cols="12"
md="2"
>
<!-- IBFT Limit {{ibft_limit}} -->
</v-col>
</v-row>


<v-row>
<v-col
cols="12"
md="2"
>
<v-btn @click="add_task">Add Task +</v-btn>
</v-col>

<v-col
cols="12"
md="4"
>

 <VueJsonToCsv class="info" :json-data="inputs">
<v-btn class="info">Export Detail</v-btn>
 </VueJsonToCsv>
</v-col>

</v-row>

</v-container>
</v-app>      
</template>
<script>
import VueJsonToCsv from '../node_modules/vue-json-to-csv'
export default {

    components : { VueJsonToCsv },    

data: () => ({
res:'',    
inputs: [{
    task:'',
    duration:0,
}],
}),
computed:{
    total(){
        return this.inputs.reduce((sum,p) => {
            return parseInt(sum) + parseInt(p.duration)
        },0)
    },
      ibft_limit () {
            return this.total  >= 666666.65 ? 500000 : (this.total/100) * 75
    }
},
created () {

    },
methods:{
save () {
   
            // this.$axios.post('transaction',{'task' : 'task', 'duration' : 321})
            //     .then(res =>  console.log(res.data) );        

                        console.log(this.inputs);
    },

deleteRow(index) {
this.inputs.splice(index,1)
},
add_task(){
this.inputs.push({
task: '',
duration: 0
});
},
}

}
</script>