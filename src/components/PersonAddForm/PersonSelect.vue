<template>
    <select v-model="value" @change="selectPerson">
        <option value="" disabled>Выберите</option>
        <option 
          v-for="option in selectOptions" 
          :key="option.id" 
          :value="option.id"
        >
            {{ option.name }}
        </option>
    </select>
</template>

<script>
export default {
    props: {
      value: String,
      selectOptions: {
        type: Array,
        required: true,
      }
    },
    methods: {
        selectPerson(event) {
            this.$emit('input', event.target.value)
            value: ''
        }
    },
}
</script>