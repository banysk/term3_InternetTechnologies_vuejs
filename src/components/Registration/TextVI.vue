<template>
	<fieldset>
		<legend v-if="legend">{{ legend }}</legend>
		<input @input="validate" type="text" v-bind:placeholder="ph" :class="{Valid : this.isValid, NotValid : isError, Validation : true}" v-model="value">
	</fieldset>
</template>

<script>
export default {
  name: 'TextVI',
  props: {
	legend: String,
	ph: String,
	min: Number,
  },
  data() {
	return {
      isValid: false,
      isError: false,
      value: null,
	}
  },
  methods: {
    validate: function() {
      if (this.value.length >= parseInt(this.min, 10)) {
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
	input {
		font-size: 18px;
		border-radius:5px;
		outline: none;
	}
	.Valid {
		border-color: green;
		border-width: 2px;
	}
	.NotValid {
		border-color: red;
		border-width: 2px;
	}
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
</style>