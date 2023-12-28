<template>
    <div>
        <h1 class="page-title">{{ titleText }}</h1>
        <hr class="title-separator">
    </div>
</template>

<script>
export default {
    props: {
        titleText: {
            type: String,
            required: true,
        },
    },
};
</script>

<style scoped>
.page-title {
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 10px;
}

.title-separator {
    width: 100%;
    border: 1px solid #ddd;
    margin-bottom: 20px;
}
</style>