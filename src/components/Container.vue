<template>
    <div class="container">
        <slot/>
    </div>
</template>

<style scoped>
.container{
    min-height:100vh;
    display: flex;
    flex-direction: column;
    margin-bottom: 150px;
    max-width: 960px;
    margin-left:auto;
    margin-right:auto;
}
</style>