<template>
  <main id="app">
    <section><img src="@/assets/logo.png" /></section>
    <Form :formFields="formFields" class="form" />
    <section class="editor">
      <div>
        <label>Select type of field</label>
      </div>
        <select v-model="field.type">
          <option v-for="(type, i) in types" :key="i" :value="type">{{type.name}}</option>
        </select>
      
      <div><label>Label</label></div>
      <input v-model="field.label" />
      
      <div><label>Field Name</label></div>
      <input v-model="field.name" />
      
      <template v-if="field.type && field.type.element == 'select'">
        <div><label>Options</label></div>
        <textarea v-model="field.options" />
      </template>
      
      <div>
        <button 
          @click="addField(field)" 
          :disabled="!field.type || !field.label || !field.name"
        >
          Add Field
        </button>
      </div>

    </section>
  </main>
</template>

<script>
import Form from './components/Form'

export default {
  name: 'App',
  components: {
    Form
  },

  data() {
    return {
      field: {},
      formFields: [],
      types: [
              {name: "input", element: "input", type: "text"},
              {name: "date", element: "input", type: "date"},
              {name: "text", element: "textarea"},
              {name: "select", element: "select"},
      ]      
    }
  },

  created() {
    this.formFields = JSON.parse(localStorage.getItem("formFields") || "[]")
  },

  methods: {
    addField(field) {
      //console.log(field) //DEBUG

      this.formFields.push(field)
      this.field = {}

      localStorage.setItem("formFields", JSON.stringify(this.formFields))
    },

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  height: 100%;
}

.form, .editor {
  width: calc(50% - 30px);
  min-height: 60vh;
  padding: 25px 5px;
  float: left;
  background-color: #e4e4e4;
  border: 10px solid white;
}

button { 
  background-color: white;
  padding: 5px 20px;
  border: none;
}

input, textarea, select {
  margin-bottom: 10px;
  min-width: 200px;
}

img { 
  height: 100px;
}
</style>
