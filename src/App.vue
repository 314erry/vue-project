<template>
    <Navbar/>
    <Hero/>
    <HomeCard/>
    <JobListings/>
</template>

<script>
    import Navbar from './components/Navbar.vue';
    import Hero from './components/Hero.vue';
    import HomeCard from './components/HomeCard.vue';
import JobListings from './components/JobListings.vue';

    export default {
        components: {
            Navbar,
            Hero,
            HomeCard,
            JobListings
        }
    }
</script>