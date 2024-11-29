<template>
    <div class="job-list">
      <div class="top-nav">
        <p>Ordered by {{ order }}</p>
        <input type="text" placeholder="Search by title..." class="searchbox" v-model="searchInp">
      </div>
        <transition-group name="list" tag="ul">
            <li v-for="job in filteredJob" :key="job.id">
                <h1>{{ job.title }} in {{ job.location }}</h1>
                <div class="salary">
                    <p>{{ job.salary }} Birr</p>
                </div>
                <div class="description">
                    <p>Lorem ipsum dolor sit amet consectetur, adipisicing elit. Vitae veritatis eius consequuntur magnam vel necessitatibus deserunt provident. Est quasi consectetur enim porro, iure voluptates ducimus deleniti totam asperiores molestias nulla.</p>
                </div>
            </li>
        </transition-group>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, PropType, ref } from 'vue'
import Job from '@/types/Job'
import OrderType from '@/types/OrderType';

export default defineComponent({
    props:{
        jobs: {
            required: true,
            type: Array as PropType<Job[]>
        },
        order: {
            required: true,
            type: String as PropType<OrderType>
        }
    },
    setup(props){
      const searchInp = ref('')

      const filteredJob = computed(()=>{
        const filterJob = searchInp.value.length > 0 ? [...props.jobs].filter((jobTitle)=>{
          return jobTitle.title.toLowerCase().includes(searchInp.value.toLowerCase())
        }): [...props.jobs]

        return filterJob.sort((a,b)=>{
          return a[props.order] > b[props.order] ? 1 : -1
        })

      })
      
      
        return { filteredJob, searchInp }
    }
})
</script>

<style scoped>
.job-list {
    max-width: 960px;
    margin: 40px auto;
  }
  .job-list ul {
    padding: 0;
  }
  .job-list li {
    list-style-type: none;
    background: white;
    padding: 16px;
    margin: 16px 0;
    border-radius: 4px;
  }
  .job-list h2 {
    margin: 0 0 10px;
    text-transform: capitalize;
  }
  .salary {
    display: flex;
  }
  .salary img {
    width: 30px;
  }
  .salary p {
    color: #17bf66;
    font-weight: bold;
    margin: 10px 4px;
  }
  .list-move{
    transition: all 1s;
  }
  .top-nav{
    display: flex;
    justify-content: space-between;
  }
  .top-nav input{
    padding: 8px 10px !important;
    width: 250px;
    height: 25px;
    border: 1px solid #cacaca;
    border-radius: 8px;
    font-size: 16px;
  }
  .top-nav input:focus{
    outline: none;
    border: 1px solid #cacaca;
  }
</style>
