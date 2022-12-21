<template>
    <div class="table">

        <div class="table-row">
          <div class="table-field-first">{{ person.name }}</div>
          <div class="table-field-second">{{ person.telephone }}</div>
        </div>

        <PersonSingle
            v-for="person in person.subordinates"
            :key="person.id"
            :person="person"
            class="table-row-child"
        />

    </div>
</template>

<script>
export default {
    name: 'PersonSingle',
  props: {
    person: {
      type: Object,
      required: true,
    },
  }
}
</script>

<style scoped>
*{
    box-sizing: border-box;
}
.table{
  display: flex;
  flex-direction: column;
}
.table-row{
  display: flex;
  flex-direction: row;
  position: relative;
  justify-content: flex-end;
}
.table-field-first{
  width: 20vw;
  padding: 20px;
  border: 2px solid #000;
}
.table-field-second{
  width: 20vw;
  padding: 20px;
  border: 2px solid #000;
}
.table-row-child{
    margin-left: 20px;
}
.table-row-child .table-field-first{
    width: calc(20vw - 20px);
}
</style>