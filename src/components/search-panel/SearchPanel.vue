<script>
export default {
    
}

</script>


<template>
        <input type="text" class="form-control search-input" @input="$emit('onSearch', $event.target.value)" placeholder="Kinolarni qidirish"/>
</template>


<style scoped>
    .search-input{
        padding: 1.5rem;
        margin-bottom: 1rem;
        background-color: #fcf5faf5;
        border-radius: 4px;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>