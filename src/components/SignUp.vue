<template>
    <h1>SignUp</h1>
    <div class="register">
        <input v-model="name" type="text" placeholder="Enter Name">
        <input v-model="email" type="email" placeholder="Enter Email">
        <input v-model="password" type="password" placeholder="Enter Password">
        <button @click="signUp">Sign Up</button>
        <p>
            <router-link to="/login">Login</router-link>
        </p>
    </div>
</template>
<script>

import axios from 'axios';
export default {
    name: "SignUp",
    data() {
        return {
            name: '',
            email: '',
            password: '',

        }
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/user", {
                name: this.name,
                email: this.email,
                password: this.password,

            })
            console.log(result)
            if (result.status == 201) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'HomePage' })   //routing to home page
            }
        }

    },
    mounted(){
        let user=localStorage.getItem('user-info')
        if(user){
             this.$router.push({ name: 'HomePage' })   //routing to home page
        }
    }
}

</script>

<style >
/* Center the whole page */
template {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
}

/* Title */
h1 {
    text-align: center;
    margin-bottom: 20px;
    font-family: Arial, Helvetica, sans-serif;
    color: #333;
}

/* Container */
.register {
    width: 400px;
    padding: 30px;
    border-radius: 12px;
    background: #f9f9f9;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

/* Inputs */
.register input {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 8px;
    outline: none;
    transition: 0.3s;
}

/* Input focus effect */
.register input:focus {
    border-color: #42b983;
    box-shadow: 0 0 5px rgba(66, 185, 131, 0.5);
}

/* Button */
.register button {
    width: 100%;
    padding: 10px;
    background: #42b983;
    color: white;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-weight: bold;
    transition: 0.3s;
}

/* Button hover */
.register button:hover {
    background: #369870;
}
</style>