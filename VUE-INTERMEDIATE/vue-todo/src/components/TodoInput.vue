<template>
  <div class="inputBox shadow">
    <input v-model="newTodoItem" type="text" @keyup.enter="addTodo">
    <span class="addContainer" @click="addTodo">
      <em class="fas fa-plus addBtn"></em>
    </span>
    <Modal v-if="showModal" @close="showModal = false">
      <h3 slot="header">경고
        <em class="closeModalBtn fas fa-times" @click="showModal = false"></em>
      </h3>
      <div slot="body">아무것도 입력하지 않으셨습니다.</div>
    </Modal>
  </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  name: "TodoInput",
  data() {
    return {
      newTodoItem: "",
      showModal: false
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoItem !== '') {
        const text = this.newTodoItem.trim();
        this.$store.commit("addOneItem", text);
        this.clearInput();
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    }
  },
  components: {
    Modal
  }
}

</script>

<style scoped>
input:focus {
  outline: none;
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

}
</style>
