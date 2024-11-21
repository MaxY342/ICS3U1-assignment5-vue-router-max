<script setup>

</script>

<template>
    <form class="login">
        <label>Username/Email</label>
        <input>
        <label>Password</label>
        <input>
        <button>Sign-up</button>
    </form>
</template>

<style scoped>
    .login {
        color: white;
        display: flex;
        flex-direction: column;
        padding: 100px;
        border-radius: 10px;
        box-shadow: 0px 8px 16px 0px rgba(0,0,0,0.2);
        gap: 10px;
    }

    input {
        height: 2rem;
    }

    button {
        background-color: #e20c0c;
        margin: 20px;
        padding: 1rem;
        color: white;
        border: 0;
        border-radius: 10px;
    }

    button:hover {
        background-color: #c20000;
        cursor: pointer;
    }

    label {
        font-size: 20px;
        margin-top: 1rem;
        margin-bottom: 1rem;
    }
</style>