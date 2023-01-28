<template>
    <select @change="this.$emit('func', $event.target.value)">
    <option  disabled selected><slot></slot></option>
    <template v-if="selectDep">
        <option v-for="(w, index) in selectedStaff" :key="index" :value="w">{{ w }}</option>
    </template>
    <template v-else v-for="workers in staff">
        <option v-for="(w, index) in workers.staff" :key="index" :value="w">{{ w }}</option>
    </template>
    </select>
</template>

<script>
    export default {
        props: ['selectDep', 'selectedStaff', 'staff']
    }
</script>