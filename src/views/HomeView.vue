<template>
    <Hero />
    <HomeCard />
    <JobListings :limit="3" :showButton="true" />
</template>

<script>
import Hero from '@/components/Hero.vue'
import HomeCard from '@/components/HomeCard.vue';
import JobListings from '@/components/JobListings.vue';

export default {
    components: {
        Hero,
        HomeCard,
        JobListings
    }
}
</script>