<template>
  <div class="table-wrapper">
    <button class="save-btn" @click="openForm">Добавить</button>

    <div class="table">
      <div class="sort-btn" @click="nameSort">Имя</div>
      <div class="sort-btn" @click="telephoneSort">Телефон</div>
    </div>

    <PersonSingle 
      v-for="person in sortedArray" 
      :key="person.id"
      :person="person"
    />

  </div>
</template>

<script>
import PersonSingle from '../components/PersonSingle.vue'

export default {
  components: {PersonSingle},
  data() {
    return {
      active: false,
      selectedSort: '',
    }
  },
  props: {
    persons: {
      type: Array,
      required: true,
    },
    activeForm: {
      type: Boolean,
      required: true,
    }
  },
  methods: {
    openForm() {
      this.$emit('open', this.active)
    },
    
    nameSort() {
      this.selectedSort = 'name';
    },
    telephoneSort() {
      this.selectedSort = 'telephone';
    },
  },
  computed: {
    sortedArray() {
      return [...this.persons].sort((person1, person2) => (person1[this.selectedSort] > person2[this.selectedSort]) ? 1 : -1)
    },
    getPersons() {
      return this.persons;
    }
  }
}
</script>

<style scoped>
.table-wrapper{
  display: flex;
  flex-direction: column;
  width: 500px;
  padding: 20px;
}
.save-btn{
  text-align: center;
  padding: 10px;
  width: 100px;
  border-radius: 50px;
  background: #ccc;
  border: 1px solid #000;
  cursor: pointer;
  margin-bottom: 20px;
}
.table{
  display: flex;
  flex-direction: row;
  width: 100%;
}
.table div{
  width: 50%;
  padding: 20px;
  border: 2px solid #000;
}
.sort-btn{
  cursor: pointer;
}
.sort-btn:hover{
  background: #ccc;
}
</style>