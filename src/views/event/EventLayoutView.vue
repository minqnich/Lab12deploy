<script setup lang="ts">
import { ref } from 'vue'
// import type { Ref } from 'vue'
// import { type EventItem } from '@/type'
// import EventService from '@/services/EventService';
// const event = ref<EventItem | null> (null)
import { useEventStore } from '@/stores/event';
import { storeToRefs } from 'pinia';
import {useRouter} from 'vue-router';

const store = useEventStore()
const event = storeToRefs(store).event
const id = ref(event?.value?.id)
const router = useRouter()

// const props = defineProps({
//     id: String
// })


    // EventService.getEventById(Number(props.id)).then((response) => {
    //     event.value = response.data
    // }).catch(error =>{
    //     console.log(error)
        // if(error.response && error.response.status === 404){
        //     router.push({name:'404-resource',params: {resource: 'event'}})
        // }else{
        //     router.push({name:'network-error'})
        // }
    // })

</script>
<template>
    <div v-if="event">
        <h1>{{ event.title }}</h1>
        <div id="nav">
            <router-link :to="{name: 'event-detail', params:{id}}">Details</router-link> >>
            <router-link :to="{name: 'event-register', params:{id}}">Register</router-link> >>
            <router-link :to="{name: 'event-edit', params:{id}}">Edit</router-link> 
        </div>
        <router-view :event="event"></router-view>
    </div>
</template>
