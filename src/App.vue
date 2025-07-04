<template>
    <Navbar/>
    <Hero/>
    <HomeCard/>
</template>

<script>
    import Navbar from './components/Navbar.vue';
    import Hero from './components/Hero.vue';
    import HomeCard from './components/HomeCard.vue';

    export default {
        components: {
            Navbar,
            Hero,
            HomeCard
        }
    }
</script>