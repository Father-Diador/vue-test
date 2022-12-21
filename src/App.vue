<template>
  <div class="wrapper">
    <PersonList 
      @open="openForm"
      :persons="persons"
      :activeForm="activeForm"
    />

    <PersonAddForm 
      @close="closeForm"
      @create="addPerson"
      v-if="activeForm"
      :activeForm="activeForm"
      :selectOptions="selectOptions"
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
        {id: 1, name: 'Марина', telephone: '+7 941 123 21 42', selectedPerson: '', subordinates: []},
        {id: 2, name: 'Петр', telephone: '+7 926 235 31 65', selectedPerson: '', subordinates: []},
        {id: 3, name: 'Алексей', telephone: '+7 903 123 21 42', selectedPerson: '', subordinates: 
          [
            {id: 4, name: 'Иван', telephone: '+7 920 123 21 42', selectedPerson: '3', subordinates: []}
          ]
        },
        {id: 5, name: 'Борис', telephone: '+7 965 123 21 42', selectedPerson: '', subordinates: []},
      ],
      selectOptions: [
        {id: 1, name: 'Марина'},
        {id: 2, name: 'Петр'},
        {id: 3, name: 'Алексей'},
        {id: 4, name: 'Иван'},
        {id: 5, name: 'Борис'},
      ],
      activeForm: false,
    }
  },
  methods: {
    findById(tree, nodeId) {
    for (let node of tree) {
        // console.log(node.id + ":" + nodeId)
        if (node.id === nodeId) return node
        // console.log(node)
        // console.log(node.subordinates)
        let subordinates = node.subordinates;
        // console.log(subordinates)
        if (!subordinates) continue;
        if (subordinates.length > 0) {
            // console.log("subordinates not null " + subordinates.length)
            let desiredNode = this.findById(subordinates, nodeId)
            if (desiredNode) return desiredNode
        } else {
            // console.log("subordinates " + subordinates.lenght)
        }
    }
    return false
    },
    addPerson(person) {

      if (person.selectedPerson !== '') {
          let head = this.findById(this.persons, Number(person.selectedPerson));
          // console.log(head);
          if (!head) {
            console.error("head not found: " + person.selectedPerson);
            return;
          }
          // console.log(head);
          head.subordinates.push(person);
          // console.log(this.persons);
      }
      else {
          console.log('ПУШ 2');
          this.persons.push(person);
      }
  
      this.selectOptions.push(person);
      
      localStorage.setItem("persons", JSON.stringify(this.persons));
      localStorage.setItem("selectOptions", JSON.stringify(this.selectOptions));
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
      localStorage.setItem("selectOptions", JSON.stringify(this.selectOptions));
    } else {
      this.persons = JSON.parse(localStorage.getItem('persons'));
      this.selectOptions = JSON.parse(localStorage.getItem('selectOptions'));
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