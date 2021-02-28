<template>
  <div class="col-md-3">
    <label :for="'select_' + label">{{ label }}</label>
    <select :id="'select_' + label" class="form-select" v-model="selected" v-on:change="update">
      <option value="" disabled selected>Selection...</option>
      <option v-for="(val, id) in array" v-bind:key="id" :value="val">{{ val }}</option>
    </select>
  </div>
</template>

<script>
export default {
  name: 'RechercheElements',
  props: ['array', 'label', 'value'],
  data () {
    return {
      selected: this.value
    }
  },
  methods: {
    update () {
      this.$emit('input', this.selected)
      this.$parent.search()
    }
  }
}
</script>
