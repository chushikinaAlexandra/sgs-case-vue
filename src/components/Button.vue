<template>
    <div>
        <button @click="this.$emit('func')" class="btn" id = "btn"><slot></slot></button>
        <!-- <button @click="this.$emit('watch')" class="btn" id = "btn1">Посмотреть cokies</button> -->
    </div>
</template>

<script>

</script>