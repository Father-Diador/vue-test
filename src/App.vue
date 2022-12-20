<template>
  <div class="wrapper">
    <PersonList 
      @open="openForm"
      :persons="persons"
      :is-active="activeForm"
    />

    <PersonAddForm 
      @close="closeForm"
      @create="addPerson"
      v-if="activeForm"
      :is-active="activeForm"
      :persons="persons"
    />
  </div>
</template>

<script>
import PersonAddForm from './components/PersonAddForm/App.vue'
import PersonList from './components/PersonList.vue'

export default {
  components: {
    PersonAddForm,
    PersonList,
  },
  data() {
    return {
      persons: [
        {id: 1, name: 'Марина', telephone: '+7 941 123 21 42', selectedPerson: ''},
        {id: 2, name: 'Петр', telephone: '+7 926 235 31 65', selectedPerson: ''},
        {id: 3, name: 'Алексей', telephone: '+7 903 123 21 42', selectedPerson: ''},
        {id: 4, name: 'Иван', telephone: '+7 920 123 21 42', selectedPerson: ''},
        {id: 5, name: 'Борис', telephone: '+7 965 123 21 42', selectedPerson: ''},
      ],
      activeForm: false,
    }
  },
  methods: {
    addPerson(person) {
      this.persons.push(person);
      localStorage.setItem("persons", JSON.stringify(this.persons));
    },

    openForm(active) {
      console.log(active)
      if (active == false) {
        this.activeForm = true;
      } else {
        this.activeForm = false;
      }
    },
    closeForm(notActive) {
      console.log(notActive)
      if (notActive == false) {
        this.activeForm = false;
      } else {
        this.activeForm = true;
      }
    },
  },
  beforeMount() {
    if (!JSON.parse(localStorage.getItem('persons'))) {
      localStorage.setItem("persons", JSON.stringify(this.persons));
    } else {
      this.persons = JSON.parse(localStorage.getItem('persons'));
    }
  }
}
</script>

<style scoped>
.wrapper{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
}
</style>