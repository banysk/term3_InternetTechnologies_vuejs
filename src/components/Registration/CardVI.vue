<template>
	<fieldset>
		<legend v-if="legend">{{ legend }}</legend>
		<input @input="validate" type="text" v-bind:placeholder="ph" :class="{Valid : this.isValid, NotValid : isError, Validation : true}" v-model="value">
	</fieldset>
</template>

<script>
export default {
  name: 'CardVI',
  props: {
	legend: String,
	ph: String,
  },
  data() {
	return {
      isValid: false,
      isError: false,
      value: null,
      sum: 0
	}
  },
  methods: {
    validate: function() {
      if (this.value.length === 16) {
        for (var i = 0; i < 16; i++) {
          let num = parseInt(this.value[15 - i] ,10);
          if (i % 2){
            num * 2 < 9 ? this.sum += num * 2 : this.sum += Math.trunc(num * 2 / 10) + (num * 2 % 10); 
          } else {
            this.sum += num;
          }
        }
		if (this.sum % 10 === 0) {
          this.$emit('validate', this.value);
          this.isValid = true;
          this.isError = false;
        } else {
          this.isValid = false;
          this.isError = true;
        }
      } else {
        this.isValid = false;
        this.isError = true;
      }
      this.sum = 0;
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
