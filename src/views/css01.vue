<template>
    <div class="testimonial-container">
        <img src="https://images.unsplash.com/photo-1570295999919-56ceb5ecca61?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=880&q=80"
            alt="user-image">
        <p class="text">
            This is simply unbelievable! I would be lost without Apple. The very
            best. Not able to tell you how happy I am with Apple.
        </p>
        <h3 class="username">Cheriser G</h3>
    </div>

</template>
<script setup>
</script>
<style scoped>
.body {
    margin: 0;
    display: flex;
    justify-content: center;
    height: 100vh;
    align-items: center;
    font-family: cursive;
    overflow-x: hidden;
}

.testimonial-container {
    width: 500px;
    height: 200px;
    background-color: slateblue;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    position: relative;
    padding: 50px 20px;
    margin: 5px;
    color: white;
    box-sizing: border-box;
}

.username {
    margin-top: 20px;
}

img {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    top: -30%;
    transform: translateX(-50%);
    left: 50%;


}

@media (max-width:720px) {
    .testimonial-container {
        margin-top: 60px;
        width: 100%;
        box-sizing: border-box;
    }
}
</style>