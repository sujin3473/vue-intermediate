<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" @keyup.enter="addTodo">
    <span class="addContainer" v-on:click.enter="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>

    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">
        경고
        <i class="closeModalBtn fas fa-times" @click="showModal = false"></i>
      </h3>

      <div slot="body">
        무언가를 입력하세요.
      </div>
    </Modal>

  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {  //공백일때는 값을 추가하지 않게 하는 로직
        this.$emit('addTodoItem', this.newTodoItem);
        this.clearInput();
      }
      else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';  //초기화 로직
    }
  },
  components: {
    Modal: Modal
  }
}
</script>

<style scoped>
  input:focus {
    outline: none;
  }
  i:hover {
    cursor: pointer;
  }
  .inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
  }
  .inputBox input {
    border-style: none;
    font-size: 0.9rem;
  }
  .addContainer {
    float: right;
    background: linear-gradient(to right, #6478FB, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
  }
  .addBtn {
    color: white;
    vertical-align: middle;
  }
  .closeModalBtn {
    color: #42b983;
    float: right;
  }
</style>