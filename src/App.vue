<template>
  <div class="app">
    <header>
      <h1>Addis Jobs</h1>
      <div class="orders">
        <button @click="handleClick('title')">order by title</button>
        <button @click="handleClick('location')">order by location</button>
        <button @click="handleClick('salary')">order by salary</button>
      </div>
    </header>
    <JobList :jobs="jobs" :order="order" />
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import Job from './types/Job'
import OrderType from './types/OrderType';
import JobList from './components/JobList.vue';

export default defineComponent({
  name: 'App',
  setup(){
    const jobs = ref<Job[]>([
      {id: '1', title: 'UI Designer', location: 'Addis Ababa', salary: 20000},
      {id: '2', title: 'Node Developer', location: 'Jimma', salary: 25000},
      {id: '3', title: 'Backend Engineer', location: 'Hawwassa', salary: 10000},
      {id: '4', title: 'PHP Developer', location: 'Dire Dawa', salary: 5000},
    ])

    const order = ref<OrderType>('title')
    const handleClick = ( term: OrderType ) => {
      order.value = term
    }

    return { jobs, order, handleClick }
  },
  components:{JobList},

});
</script>

<style>
header {
    text-align: center;
  }
  header .order {
    margin-top: 20px;
  }
  button {
    margin: 0 10px;
    color: #1195c9;
    border: 3px solid #1195c9;
    background: #d5f0ff;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: bold;
  }
</style>
