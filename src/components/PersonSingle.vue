<template>
    <div class="table">
        <div>{{ person.name }}</div>
        <div>{{ person.telephone }}</div>
        <div>{{ person.selectedPerson }}</div>
    </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object,
      required: true,
    },
  }
}
</script>

<style scoped>
.table{
  display: flex;
  flex-direction: row;
}
.table div{
  width: 33%;
  padding: 20px;
  border: 2px solid #000;
}
</style>