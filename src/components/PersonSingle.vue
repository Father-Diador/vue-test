<template>
    <div class="table">

        <div class="table-row">
          <div class="table-field">{{ person.name }}</div>
          <div class="table-field">{{ person.telephone }}</div>
        </div>

        <div
          v-for="subordinates in person.subordinates"
          :key="subordinates.id"
          class="table-row-subordinate"
        >
          <div class="table-row-subordinate-row">
            <div class="table-field-subordinate">{{ subordinates.name }}</div>
            <div class="table-field">{{ subordinates.telephone }}</div>
          </div>
          
          <div
            v-for="subordinates in subordinates.subordinates"
            :key="subordinates.id"
            class="table-row-subordinate"
          >
            <div class="table-row-subordinate-row">
              <div class="table-field-subordinate">{{ subordinates.name }}</div>
              <div class="table-field">{{ subordinates.telephone }}</div>
            </div>

          </div>

        </div>

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
  flex-direction: column;
}
.table-row{
  display: flex;
  flex-direction: row;
}
.table-row-subordinate{
  display: flex;
  flex-direction: column;
  width: 100%;
}
.table-row-subordinate-row{
  display: flex;
  flex-direction: row;
  width: 100%;
}
.table-field{
  width: 50%;
  padding: 20px;
  border: 2px solid #000;
}
.table-field-subordinate{
  margin-left: 10%;
  width: 40%;
  padding: 20px;
  border: 2px solid #000;
}
</style>