<template>
  <button :class="classes" @click="onClick">
	  Test Button
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Button extends Vue {
	@Prop({ type: Boolean, default: false }) disabled!: boolean;

	get classes(): object {
		return {
			'my-button': true,
			'my-button--disabled': this.disabled
		};
	}

	onClick(): void {
		if (!this.disabled) {
			this.$emit('click');
		}
	}
}
</script>

<style scoped lang="scss">
.my-button {
	background: rgb(13, 13, 102);
	color: white;
	border-radius: 50px;
	padding: 0 20px;
	line-height: 35px;
	border: unset;
    cursor: pointer;

	&--disabled {
		background: grey;
		pointer-events: none;
	}
}
</style>
