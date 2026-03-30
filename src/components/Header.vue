<template>
    <nav class="navbar">
        <div class="logo">
            <img :src="logo" alt="Logo">
        </div>
        <div class="nav-links">
            <router-link to="/"> Home</router-link>
            <router-link to="/add">Add Restaurant</router-link>
            <a @click="logout" href="#">Log Out</a>
        </div>
    </nav>
</template>

<script>
import logo from '@/assets/rest.jpg'
export default {
    name: 'Header',
    methods: {
        logout() {
            localStorage.clear();
            this.$router.push({ name: "Login" })

        }

    },
    data() {
        return {
            logo
        }
    }
}
</script>

<style scoped>
/* Navbar container */
.navbar {
    width: 100%;
    height: 150px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 10px -15px;
    background: linear-gradient(90deg, #42b983, #2c3e50);
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    position: fixed;
    top: 0;
    left: 0;

    border-bottom-left-radius: 12px;
    border-bottom-right-radius: 12px;
    transition: 0.3s;
}

/* Logo section */
.logo {
    display: flex;
    align-items: center;
    gap: 10px;
    color: white;
    font-weight: bold;
    font-family: Arial, Helvetica, sans-serif;
}

.logo img {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    border: 2px solid white;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
    transition: 0.3s;
}



/* Links container */
.nav-links {
    display: flex;
    gap: 20px;
    margin-right: 30px;
}

.nav-links a {
    color: white;
    text-decoration: none;
    font-weight: bold;
    font-size: 16px;
    padding: 8px 10px;
    border-radius: 8px;
    transition: 0.3s;
}

.nav-links a:hover {
    background: rgba(255, 255, 255, 0.2);
    transform: scale(1.05);
}

/* Active link style (optional) */
.nav-links a.active {
    border-bottom: 2px solid white;
}

/* Adjust spacing for page content below navbar */
body,
.app-container {
    padding-top: 50px;
    /* equal or bigger than navbar height */
}
</style>