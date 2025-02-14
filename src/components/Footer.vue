<template>
    <div class="footer">
        <RouterLink to="/dashboard">&copy; 2025 Sky7Dev. All rights reserved.</RouterLink>
    </div>
</template>

<script>
    export default {
        name: "Footer",
    }
</script>

<style lang="css" scoped>
    .footer {
        background-color: #06195c;
        color: white;
        text-align: center;
        padding: 1rem;
        margin-top: 2rem;
    }
    .footer p {
        margin: 0;
    }
    a {
        color: white;
    }
</style>