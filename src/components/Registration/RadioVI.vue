<template>
	<fieldset>
		<legend v-if="legend" :class="{Valid : this.isValid, NotValid : isError, Validation : true}">{{ legend }}</legend>
		<ul>
          <li v-for="gender in list" v-bind:key="gender">
          <input @change="validate" type="radio" v-bind:name="group_name" :value="gender" v-model="value"/>{{gender}}
          </li>
		</ul>
	</fieldset>
</template>

<script>
export default {
  name: 'RadioVI',
  props: {
	legend: String,
	group_name: String,
	list: {},
  },
  data() {
    return {
      isValid: false,
      isError: true,
      value: null,
	};
  },
  methods: {
    validate: function() {
      if (this.value) { 
        this.$emit('validate', this.value);
        this.isValid = true;
        this.isError = false;
      } else {
        this.isValid = false;
        this.isError = true;
      }
	}
  }
}
</script>

<style scoped>
	div fieldset {
		border-radius: 10px;
		font-size: 18px;
		opacity: .85;
		margin-bottom: 2%;
		width: 80%;
	}
	div fieldset:hover {
		opacity: 1.0;
	}
	ul {
      list-style-type: none;
      text-align: left;
      margin: 0;
	}
</style>
