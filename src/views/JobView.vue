<template>
    <BackButton />
    <section v-if="!isLoading" class="bg-green-50">
        <div class="container m-auto py-10 px-6">
            <div class="grid grid-cols-1 md:grid-cols-[70%_30%] w-full gap-6">
                <main>
                    <div class="bg-white p-6 rounded-lg shadow-md text-center md:text-left">
                        <div class="text-gray-500 mb-4">{{ job.type }}</div>
                        <h1 class="text-3xl font-bold mb-4">{{ job.title }}</h1>
                        <div class="text-gray-500 mb-4 flex align-middle justify-center md:justify-start">
                            <div class="text-orange-700 mb-3">
                                <i class="pi pi-map-marker text-orange-700"></i>
                                {{ job.location }}
                            </div>
                        </div>
                    </div>

                    <div class="bg-white p-6 rounded-lg shadow-md mt-6">
                        <h3 class="text-green-800 text-lg font-bold mb-6">
                            Job Description
                        </h3>

                        <p class="mb-4">
                            {{ job.description }}
                        </p>

                        <h3 class="text-green-800 text-lg font-bold mb-2">Salary</h3>

                        <p class="mb-4">{{ job.salary }}</p>
                    </div>
                </main>

                <!-- Sidebar -->
                <aside>
                    <!-- Company Info -->
                    <div class="bg-white p-6 rounded-lg shadow-md">
                        <h3 class="text-xl font-bold mb-6">Company Info</h3>

                        <h2 class="text-2xl">{{ job.company.name }}</h2>

                        <p class="my-2">
                            {{ job.company.description }}
                        </p>

                        <hr class="my-4" />

                        <h3 class="text-xl">Contact Email:</h3>

                        <p class="my-2 bg-green-100 p-2 font-bold">
                            {{ job.company.contactEmail }}
                        </p>

                        <h3 class="text-xl">Contact Phone:</h3>

                        <p class="my-2 bg-green-100 p-2 font-bold">{{ job.company.contactPhone }}</p>
                    </div>

                    <!-- Manage -->
                    <div class="bg-white p-6 rounded-lg shadow-md mt-6">
                        <h3 class="text-xl font-bold mb-6">Manage Job</h3>
                        <RouterLink :to="`/jobs/edit/${job.id}`"
                            class="bg-green-500 hover:bg-green-600 text-white text-center font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block">
                            Edit
                            Job</RouterLink>
                        <button @click="deleteJob"
                            class="bg-red-500 hover:bg-red-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline mt-4 block">
                            Delete Job
                        </button>
                    </div>
                </aside>
            </div>
        </div>
    </section>

    <div v-else class="text-center text-gray-500 py-6">
        <PulseLoader />
    </div>
</template>

<script>
import axios from 'axios'
import PulseLoader from 'vue-spinner/src/PulseLoader.vue'
import { RouterLink } from 'vue-router'
import BackButton from '@/components/BackButton.vue'

export default {
    components: {
        PulseLoader,
        BackButton
    },

    data() {
        return {
            job: [],
            jobId: this.$route.params.id,
            isLoading: true
        }
    },


    async mounted() {
        try {
            const response = await axios.get(`/api/jobs/${this.jobId}`);
            this.job = response.data;
        } catch (error) {
            console.error('Error fetching job', error);
        } finally {
            this.isLoading = false;
        }
    },

    methods: {
        async deleteJob() {
            try {
                await axios.delete(`/api/jobs/${this.jobId}`);
                this.$router.push('/jobs')
            } catch (error) {
                console.log('Error deleting job', error)
            }
        }
    }
}
</script>