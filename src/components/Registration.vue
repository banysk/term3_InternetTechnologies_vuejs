<template>
	<div>
		<h1 @mouseover="joke" @mouseleave="notJoke" :key="this.header"> {{ this.header }} </h1>
		<h4>Registration</h4>
		<form @submit.prevent="validate" action="">
			<RadioVI @validate="getGender" legend="What is Your gender?" v-bind:list="['Male', 'Female', 'Battle Helicopter']" group_name="gender"></RadioVI>
			<TextVI @validate="getName" legend="What is Your name?" ph="Billy" min="2"></TextVI>
			<TextVI @validate="getLang" legend="What is Your favourite programming language?" ph="Python" min="1"></TextVI>
			<PhoneVI @validate="getPhone" legend="What is Your phone number?" ph="+7XXXXXXXXXX"></PhoneVI>
			<CardVI @validate="getCard" legend="What is Your credit card number?" ph="XXXXXXXXXXXXXXXX"></CardVI>
			<h5 v-bind:class="{Hidden : !attention, NotHidden : attention}">Wrong data!!!</h5>
			<button>Register</button>
		</form>
	</div>
</template>

<script>
import RadioVI from '@/components/Registration/RadioVI.vue'
import TextVI from '@/components/Registration/TextVI.vue'
import PhoneVI from '@/components/Registration/PhoneVI.vue'
import CardVI from '@/components/Registration/CardVI.vue'
export default {
  name: 'Registration',
  components: {
    RadioVI,
	PhoneVI,
	TextVI,
	CardVI,
  },
  methods: {
    joke: function() {
      this.header = "Grыndr";
	},
	notJoke: function() {
      this.header = "Tыnder";
    },
    validate: function() {
      var Validation_c = document.getElementsByClassName("Validation").length;
      var Validated_c = document.getElementsByClassName("Valid").length;
      this.attention = (Validation_c != Validated_c);
      if (!this.attention) {
		this.$emit('registration', this.user_data);
      }
	},
    getGender: function(event) {
        this.user_data.gender = event;
    },
	getName: function(event) {
        this.user_data.name = event;
    },
    getLang: function(event) {
        this.user_data.lang = event;
    },
    getPhone: function(event) {
        this.user_data.phone = event;
    },
    getCard: function(event) {
        this.user_data.card = event;
    }
  },
  data() {
    return {
      attention: false,
      header: "Tыnder",
      user_data: {
        gender: null,
        name: null,
        lang: null,
        phone: null,
        card: null
      }
	};
  }
}
</script>

<style scoped>
	div {
		width: 55%;
		opacity: .9;
		border-radius: 30px;
		background-color: #fad0c4;
		background-image: linear-gradient(315deg, #fad0c4 0%, #f1a7f1 74%);
	}
	div h1 {
		font-size: 100px;
		padding: 0px;
		margin: 0px;
		font-weight: 700;
		cursor: default;
	}
	div h4 {
		font-size: 40px;
		padding: 0px;
		margin: 0 0 1% 0;
		font-weight: 100;
		cursor: default;
	}
	button {
		font-size: 20px;
		border-radius: 5px;
		border-width: 1px;
		margin-bottom: 1%;
        outline: none;
	}
	.Hidden {
        display: none;
    }
	.NotHidden {
        display: block;
        font-weight: 100;
        color: red;
		font-size: 20px;
		margin: 1%;
		padding: 0;
	}
</style>
