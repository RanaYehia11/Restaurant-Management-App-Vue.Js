<template>
    <Header />

    <div class="page">
        <div class="form-card">
            <h1>Add Restaurant 🍽️</h1>

            <form class="add">
                <input v-model="restaurant.name" type="text" placeholder="Restaurant Name" />

                <input v-model="restaurant.address" type="text" placeholder="Restaurant Address" />

                <input v-model="restaurant.contact" type="number" placeholder="Contact Number" />

                <button @click="addRest" type="button">
                    Add New Restaurant
                </button>
            </form>
        </div>
    </div>
</template>

<script>
import Header from "@/components/Header.vue"
import axios from "axios";
export default {
    name: "AddPage",
    components: {
        Header,

    },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: '',
            }
        }
    },
    methods: {
        async addRest() {
            const result = await axios.post("http://localhost:3000/restaurant",
                {
                    name: this.restaurant.name,
                    address: this.restaurant.address,
                    contact: this.restaurant.contact
                });
            console.log(result)
            if (result.status == 201) {
                this.$router.push({ name: "HomePage" })
            }

        }
    },


}
</script>

<style >
/* Page layout */
.page {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 40px;
    background: #f5f7fa;
    min-height: 70vh;


}

/* Card */
.form-card {
    width: 400px;
    background: white;
    padding: 30px;
    border-radius: 16px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
    text-align: center;
}

/* Title */
h1 {
    margin-bottom: 25px;
    color: #2c3e50;
}

/* Form */
.add {
    display: flex;
    flex-direction: column;
}

/* Inputs */
.add input {
    padding: 12px;
    margin: 10px 0;
    border: 1px solid #ddd;
    border-radius: 8px;
    transition: 0.3s;
    font-size: 14px;
}

/* Focus */
.add input:focus {
    border-color: #42b983;
    box-shadow: 0 0 5px rgba(66, 185, 131, 0.4);
    outline: none;
}

/* Button */
.add button {
    margin-top: 15px;
    padding: 12px;
    background: linear-gradient(135deg, #42b983, #2c3e50);
    color: white;
    border: none;
    border-radius: 8px;
    font-weight: bold;
    cursor: pointer;
    transition: 0.3s;
}

/* Hover */
.add button:hover {
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

/* Active click */
.add button:active {
    transform: scale(0.98);
}
</style>