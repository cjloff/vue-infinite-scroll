<template>
    <div class="card">
        {{ item }}
    </div>
</template>

<script>
export default {
    props: {
        item: {
            type: Number,
            required: true
        }
    }
}

</script>

<style>
.card {
    padding: 30px;
    background-color: #eee;
    height: 180px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2rem;
    font-weight: bold;
}
</style>
