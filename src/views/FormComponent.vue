<template>
    <form @submit.prevent :class="{blurred: isBlurred}"  >
      <h4 >Налаштування користувача</h4>
      <v-input  
        v-model="post.name"
        type="text"
        placeholder="Iм'я"
      />
      <v-warning v-if="isCreateClicked && !this.post.name" fieldName="name"/>

      <v-input
        v-model="post.surname"
        type="text"
        placeholder="Прiзвище"
      />
      <v-warning v-if="isCreateClicked && !this.post.surname" fieldName="surname"/>
      
      <v-input
        v-model="post.login"
        type="text"
        placeholder="Логiн"
        /> 
      <v-warning v-if="isCreateClicked && !this.post.login" fieldName="login"/>
      
      <v-input
        v-model="post.password"
        type="password"
        placeholder="Пароль"
      /> 
      <v-warning v-if="isCreateClicked && !this.post.password" fieldName="password"/>

      <div>
        <h4>Категорії</h4>
        <v-checkbox value="medicine" v-model="post.selectedCategories">Лiки</v-checkbox>
        <v-checkbox value="food"     v-model="post.selectedCategories">Їжа</v-checkbox>
        <v-checkbox value="gadgets"  v-model="post.selectedCategories">Гаджети</v-checkbox>
      </div>
      <v-warning v-if="isCreateClicked && this.post.selectedCategories.length < 1" fieldName="categories"/>
      {{post.selectedCategories}}!

      <div>
        <h4>Операції</h4>
        <v-radio value="create" v-model="post.operations">Створення</v-radio>
        <v-radio value="update" v-model="post.operations">Оновлення</v-radio>
        <v-radio value="relocate" v-model="post.operations">Перемiщення</v-radio>
        <v-radio value="delete" v-model="post.operations">Видалення</v-radio>
      </div>
      <v-warning v-if="isCreateClicked && !this.post.operations" fieldName="operations"/>

      <div>
        <v-checkbox  
                                v-model="secondWorker"
                                @click="toggle"
        >Робiтник другої змiни</v-checkbox>
        {{secondWorker}}
      </div>

      <v-spinner v-if="isFilledCheck() && isCreateClicked"/>

      <v-button @click="createPost" />
      
    </form>
  </template>
  
<script>
import VCheckbox from '@/components/v-checkbox.vue';
import VInput from '@/components/v-input.vue';
import VRadio from '@/components/v-radio.vue';
import VButton from '@/components/v-button.vue';
import VWarning from '@/components/v-warning.vue';
import VSpinner from '@/components/v-spinner.vue'

  export default {
    name: "FormComponent",
    components: { VCheckbox, VInput, VRadio, VButton, VWarning, VSpinner },
    data() {
        return {
          post: {
            name: "",
            surname: "",
            login: "",
            password: "",
            selectedCategories: [],
            operations: null,
          },
          secondWorker: false,
          isCreateClicked: false,
          isBlurred: false,

        };
    },
    methods: {
      isFilledCheck() {
        return this.post.name && this.post.surname && this.post.login 
        && this.post.password && (this.post.selectedCategories.length > 0) && this.post.operations
          ? true : false
        
        // let res = new Set();
        // Object.values(this.post).map(v => !!v ? res.add(true) : res.add(false))
        // return res.size === 1 ? true : false
      },
      toggle() {this.post.secondWorker = !this.post.secondWorker},
      createPost() {
        this.isCreateClicked = true;
        if (this.isCreateClicked && !this.isFilledCheck()) return;
        
        let _post = this.post;
        _post.id = Date.now();
        _post['secondWorker'] = this.secondWorker;
        
        this.isBlurred = true;
        console.log(_post, this.isBlurred);
        setTimeout(() => console.log('unblurred'),2000)
        this.isBlurred = false
        
        this.post = {
          name: "",
          surname: "",
          login: "",
          password: "",
          selectedCategories: [],
          operations: "",
        };
        this.secondWorker = false;
        this.isCreateClicked = false;
        this.$emit("create", _post); // here will be post-req
      }
    },
}
  </script>
  
  <style scoped>
  form {
    display: flex;
    flex-direction: column;
  }
  .blurred {
    /* backdrop-filter: blur(3px); */
    filter: blur(1px);
    /* opacity: 50%; */
  }
  
  </style>