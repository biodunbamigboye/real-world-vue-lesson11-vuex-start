<template>
 <div>
  <h1>Create Event {{ user.name }}</h1>
  <p> This event was created by {{ user.id }}</p>
  <ul>
   <li v-for="cat in categories" :key="cat">{{cat }}</li>
  </ul>
  <p>There are {{catLength }} categories</p>
  <p>{{ getEventById(3) }}</p>
  <button v-on:click="INCREMENT_COUNT" >Current Count is {{ count }}</button>
  <input type="number" v-model.number="incrementer" @change="INCREMENT_COUNT" placeholder="Enter Increment Value">
 
 </div>
</template>
<script>
import { mapState,mapGetters  }  from 'vuex'
import DatePicker from 'vuejs-datepicker'
export default{
  components:{
    DatePicker
  },
  data(){
    return { 
      incrementer: 0
      }
  },
computed : {
  getEventById (){return this.$store.getters.getEventById },
  catLength() {return this.$store.getters.catLength},
  
  ...mapGetters(['getEventById']),
  ...mapState(['user','categories','count'])
},
methods : {
INCREMENT_COUNT(){
  this.$store.dispatch('updateCount',this.incrementer)
},
}


}
</script>
