<template>
    <div class="testimonial-container">
        <img src="https://images.unsplash.com/photo-1570295999919-56ceb5ecca61?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=880&q=80"
            alt="user-image">
        <p class="text">
            This is simply unbelievable! I would be lost without Apple. The very
            best. Not able to tell you how happy I am with Apple.
        </p>
        <h4 class="username">Cheriser G</h4>
    </div>
</template>
<script setup>
</script>
<style scoped>
body {
    margin: 0;
    display: flex;
    height: 100vh;
    align-items: center;
    font-family: cursive;
}
.testimonial-container{
    width: 500px;
    height: 100px;
    background-color: slateblue;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    min-width: 400px;
    padding: 70px 20px;
    margin: 5px;
    color: white;
    position: relative;
}
img{
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
    top: -50%;
}
</style>