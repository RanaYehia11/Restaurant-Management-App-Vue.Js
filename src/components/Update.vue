<template>
    <Header />

    <div class="page">
        <div class="form-card">
            <h1>Update Restaurant 🍽️</h1>

            <form class="add">
                <input v-model="restaurant.name" type="text" placeholder="Restaurant Name" />

                <input v-model="restaurant.address" type="text" placeholder="Restaurant Address" />

                <input v-model="restaurant.contact" type="number" placeholder="Contact Number" />

                <button @click="updRest" type="button">
                    Update Restaurant
                </button>
            </form>
        </div>
    </div>
</template>

<script>

import Header from "@/components/Header.vue"
import axios from "axios";
export default {
    name: "UpdatePage",
    components: {
        Header,

    },
    data() {
        return {
            restaurant: {
                id: '',
                name: '',
                address: '',
                contact: '',
            }
        }
    },
    methods: {
        async updRest() {
            const result = await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,
                {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact
                });
            console.log(result)
            if (result.status == 200) {
                this.$router.push({ name: "HomePage" })
            }

        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info')
        if (!user) {
            this.$router.push({ name: 'SignUp' })   //routing to home page
        }
        // need to revise well
        const result = await axios.get('http://localhost:3000/restaurant/' + this.$route.params.id)
        console.log(result)
        this.restaurant = result.data
    }
}
</script>