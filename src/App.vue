<script>
import HeaderTemplate from './components/Header.vue'
import FooterTemplate from './components/Footer.vue'
import ArduinoControl from './components/ArduinoControl.vue'

export default {
  name: 'App',
  components: {
	HeaderTemplate,
	FooterTemplate,
	ArduinoControl
  }
};
</script>

<style>
  @import './assets/styles/Form.css';
  @import './assets/styles/Header.css';
  @import './assets/styles/Footer.css';
</style>

<template>
	<div id="app" class="d-flex flex-column justify-content-between">
		<HeaderTemplate></HeaderTemplate>
		<ArduinoControl  />
		<FooterTemplate></FooterTemplate >
	</div>
</template>