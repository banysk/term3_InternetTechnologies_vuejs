<template>
	<center>
		<Registration @registration="getData"></Registration>
	</center>
</template>

<script>
import Registration from '@/components/Registration.vue'

export default {
  name: 'App',
  components: {
    Registration
  },
  methods: {
    getData: function(event) {
        this.UserData = event;
		console.log(this.UserData);
    }
  },
  data() {
      return {
          UserData : []
      };
  }
}
</script>

<style>

</style>
