<template>
    <h1>Log in</h1>
    <div class="login">
        <input v-model="email" type="email" placeholder="Enter Email">
        <input v-model="password" type="password" placeholder="Enter Password">
        <button @click="login">Log in</button>
        <p>
            <router-link to="/signup">Sign up</router-link>
        </p>
    </div>
</template>
<script>

import axios from 'axios';
export default {
    name: "Login",
    data() {
        return {
            email: '',
            password: '',

        }
    },
    methods: {
        async login() {
            try {
                let result = await axios.get(
                    `http://localhost:3000/user?email=${this.email.trim()}`
                )

                if (result.data.length > 0) {
                    let user = result.data[0]

                    if (user.password === this.password.trim()) {
                        localStorage.setItem("user-info", JSON.stringify(user))
                        this.$router.push({ name: 'HomePage' })
                    } else {
                        alert("Wrong password ❌")
                    }

                } else {
                    alert("Email not found ❌")
                }

            } catch (error) {
                console.error(error)
                alert("Server error ❌")
            }
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info')
        if (user) {
            this.$router.push({ name: 'HomePage' })   //routing to home page
        }
    }
}

</script>


<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
}

/* Main layout */
.app-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    height: 140vh;
    background: linear-gradient(135deg, #42b983, #2c3e50);
}

/* Logo styling */
.logo {
    width: 150px;
    height: 150px;
    object-fit: cover;
    border-radius: 50%;
    /* makes it circle */
    margin-bottom: 20px;
    border: 4px solid white;
    box-shadow: 0 6px 20px rgba(0, 0, 0, 0.25);
    transition: 0.3s;
}

/* Hover effect */
.logo:hover {
    transform: scale(1.08) rotate(3deg);
}

/* Optional: make signup card look better on gradient */
.register {
    background: white !important;
}

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
.login {
    width: 400px;
    padding: 30px;
    border-radius: 12px;
    background: #f9f9f9;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
}

/* Inputs */
.login input {
    width: 100%;
    padding: 10px;
    margin: 10px 0;
    border: 1px solid #ccc;
    border-radius: 8px;
    outline: none;
    transition: 0.3s;
}

/* Input focus effect */
.login input:focus {
    border-color: #42b983;
    box-shadow: 0 0 5px rgba(66, 185, 131, 0.5);
}

/* Button */
.login button {
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
.login button:hover {
    background: #369870;
}
</style>
