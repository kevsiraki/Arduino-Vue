<template>
	<div class="wrapper">
		<h2 id="info-two" class="darkable-text">LED Controls</h2>
		<br>
		<div v-if="show" :class="alertClass">
			<span >{{ update }}</span>
		</div>
		<div v-if="show" class="center alert alert-secondary">
			<span>{{ red }}</span>
			<br>
			<span> {{ blue }}</span>
			<br>
			<span>{{ orange }}</span>
		</div>
		<br>
		<button class = "btn btn-danger" @click="ledUpdate('RH')">Red On</button>&nbsp;&nbsp;
		<button class = "btn btn-secondary" @click="ledUpdate('RL')">Red Off</button><br><br>
		<button class = "btn btn-primary" @click="ledUpdate('BH')">Blue On</button>&nbsp;&nbsp;
		<button class = "btn btn-secondary" @click="ledUpdate('BL')">Blue Off</button><br><br>
		<button class = "btn btn-warning" @click="ledUpdate('OH')">Orange On</button>&nbsp;&nbsp;
		<button class = "btn btn-secondary" @click="ledUpdate('OL')">Orange Off</button>
		<br>
	</div>
</template>

<script>
import axios from 'axios';

export default {
	name: 'ArduinoControl',
	data() {
		return  {
			alertClass: 'center alert alert-primary', 
			show: false,
			update: '',
			red: '',
			blue: '',
			orange: ''
		}
	},
	methods: {
		ledUpdate(action) {
			axios.get('http://local_ip?action='+action)
			.then(response => response.data)
			.then(data => {
				if(data.LED_UPDATE.includes("Red"))
				{
					this.alertClass = 'center alert alert-danger';
				}
				else if(data.LED_UPDATE.includes("Blue"))
				{
					this.alertClass = 'center alert alert-primary';
				}
				else if(data.LED_UPDATE.includes("Orange"))
				{
					this.alertClass = 'center alert alert-warning';
				}
				this.update =  data.LED_UPDATE;
				this.red = "Red: " + data.Red;
				this.blue = "Blue: " +  data.Blue;
				this.orange = "Orange: " +  data.Orange;
				this.show = true;
			})
			.catch(err => {
				console.error(err);
			});
		}
	}
};
</script>