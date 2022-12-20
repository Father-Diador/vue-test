<template>
    <select v-model="value" @change="selectPerson">
        <option value="" disabled>Выберите</option>
        <option 
          v-for="person in persons" 
          :key="person.id" 
          :value="person.name"
        >
            {{ person.name }}
        </option>
    </select>
</template>

<script>
export default {
    props: {
      value: String,
      persons: {
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