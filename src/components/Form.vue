<template>
  <main :key="id_form">
  
      <div v-for="field in formFields" :key="field.name">
        <div>{{field.label}}</div>
        <component 
          :is="field.type.element" 
          :type="field.type.type"
          :value="form[field.name]"
          @input="(event)=>setData(field.name, event)"
        >
          <template v-if="field.type.element == 'select' && field.options">
            <option></option>
            <option v-for="option in field.options.split(/\n/)" :key="option">{{option}}</option>
          </template>
        </component>
      </div>

    <section>
      <button @click="clear" :disabled="!formFields.length">Clear Form</button>
      <button @click="submit" :disabled="!formFields.length">Submit</button>
    </section>
    
  </main>
</template>

<script>
export default {
  name: 'Form',
  props: ['formFields'],

  data () {
    return {
      form: {},
      id_form: 0
    }
  },

  methods: {
    submit() {
      console.log(this.form);
    },

    clear() {
      this.form = {}
      this.id_form++
    },

    setData(name, event) {
      this.form[name] = event.target.value // v-model
    }
  }
}
</script>

<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
