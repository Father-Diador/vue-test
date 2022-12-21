<template>
  <div>
    <form @submit.prevent class="form-wrapper">

      <div class="tile-and-close">
        <h4>Добавление пользователя</h4>
        <button @click="closeForm">x</button>
      </div>

      <div class="input-position">
        <label for="name">Имя</label>
        <input 
          name="name" 
          type="text"
          v-model="person.name"
          placeholder="Введите имя"
        >
      </div>

      <div class="input-position">
        <label for="telephone">Телефон</label>
        <input 
          name="telephone" 
          type="text" 
          v-model="person.telephone"
          placeholder="Введите телефон"
        >
      </div>

      <div class="input-position">
        <label for="">Начальник</label>
        <PersonSelect 
          :selectOptions="selectOptions"
          v-model="person.selectedPerson"
        />
      </div>
      
      <button class="save-btn" @click="addPerson">Сохранить</button>

    </form>
  </div>
</template>

<script>
import PersonSelect from './PersonSelect.vue'

export default {
  components: {PersonSelect},
  data() {
    return {
      notActive: false,
      person: {
        name: '',
        telephone: '',
        selectedPerson: '',
        subordinates: [],
      },
    }
  },
  props: {
    selectOptions: {
      type: Array,
      required: true,
    },
    activeForm: {
      type: Boolean,
      required: true,
    }
  },
  methods: {
    addPerson() {
      if (this.person.name !== '' && this.person.telephone !== '') {
        this.person.id = Date.now();
        this.$emit('create', this.person)
        this.person = {
          name: '',
          telephone: '',
          selectedPerson: '',
          subordinates: [],
        }
      } else {
        alert('Ошибка! Поля не заполнены!')
      }
    },
    closeForm() {
      this.$emit('close', this.notActive)
    }
  }
}
</script>

<style scoped>
.form-wrapper{
  display: flex;
  flex-direction: column;
  width: 500px;
  padding: 20px;
  border: 2px solid #000;
}
.tile-and-close{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
}
.tile-and-close button{
  cursor: pointer;
  background: transparent;
  border: none;
  padding: 0;
}
.input-position{
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  margin: 10px 0px 10px 0px;
}
.input-position label{
  width: 20%;
}
.input-position input, select{
  width: 70%;
  padding: 5px;
  border: 1px solid #000;
}
.save-btn{
  text-align: center;
  padding: 10px;
  width: 100px;
  border-radius: 50px;
  cursor: pointer;
}
</style>