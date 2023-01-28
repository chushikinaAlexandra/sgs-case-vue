<template>
  <div class="app">
    <SelectForm 
    :towns="towns" 
    :departments="departments"
    :staff="staff"
    ></SelectForm>
  </div>
</template>

<script>
import SelectForm from "@/components/SelectForm.vue"
import Select from "@/components/SelectForm.vue"

export default {
  components: {
    SelectForm, Select
  },
}
</script>

<style>

</style>
