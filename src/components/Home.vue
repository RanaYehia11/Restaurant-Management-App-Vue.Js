<template>
    <Header></Header>

    <div class="home">
        <h1>Hello {{ name }}, Welcome 👋</h1>

        <div class="table-container">
            <table>
                <thead>
                    <tr>

                        <th>Name</th>
                        <th>Address</th>
                        <th>Contact</th>
                        <th>Actions</th>
                    </tr>
                </thead>

                <tbody>
                    <tr v-for="item in restaurant" :key="item.id">

                        <td>{{ item.name }}</td>
                        <td>{{ item.address }}</td>
                        <td>{{ item.contact }}</td>
                        <td>
                            <router-link class="update-btn" :to="'/update/' + item.id">Update</router-link>

                            <button class="delete-btn" @click="deleteRest(item.id)">
                                Delete
                            </button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios';
export default {
    name: "HomePage",
    data() {
        return {
            name: '',
            restaurant: [],
        }
    },
    components: {
        Header,
    },
    methods: {
        async deleteRest(id) {
            let result = await axios.delete('http://localhost:3000/restaurant/' + id)
            if (result.status == 200) {
                this.loadData();
            }

        },
        async loadData() {
            let user = localStorage.getItem('user-info')
            this.name = JSON.parse(user).name;
            if (!user) {
                this.$router.push({ name: 'SignUp' })   //routing to signup page if not user
            }
            let result = await axios.get('http://localhost:3000/restaurant')
            console.log(result)
            this.restaurant = result.data;
        }

    },
    async mounted() {
        this.loadData();

    }
}

</script>
<style scoped>
h1 {


    color: #2c3e50;
}

/* Table container */
.table-container {

    background: white;
    padding: 20px;
    border-radius: 12px;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.1);
    overflow-x: auto;
}

/* Table */
table {
    width: 100%;
    border-collapse: collapse;
    font-family: Arial, Helvetica, sans-serif;
}

/* Header */
thead {
    background: #42b983;
    color: white;
}

th {
    padding: 12px;
    text-align: left;
}

/* Rows */
td {
    width: 160px;
    height: 40px;
    padding: 12px;
    border-bottom: 1px solid #eee;
}

/* Zebra effect */
tbody tr:nth-child(even) {
    background: #f9f9f9;
}

/* Hover effect */
tbody tr:hover {
    background: #e6f7f1;
    transition: 0.3s;
}

.update-btn {
    background: #3498db;
    color: white;
    padding: 6px 12px;
    border-radius: 6px;
    text-decoration: none;
    margin-right: 8px;
    font-size: 13px;
    transition: 0.3s;
}

.update-btn:hover {
    background: #2c80b4;
}


.delete-btn {
    background: #e74c3c;
    color: white;
    border: none;
    padding: 6px 12px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 13px;
    transition: 0.3s;
}

/* Hover */
.delete-btn:hover {
    background: #c0392b;
    transform: scale(1.05);
}

/* Click effect */
.delete-btn:active {
    transform: scale(0.95);
}
</style>