<template>
  <button :class="classes" @click="onClick">
	  Test Button
      <span class="tooltiptext">Hov Tooltip Text</span>
  </button>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class Button extends Vue {
	@Prop({ type: Boolean, default: false }) disabled!: boolean;

	get classes(): object {
		return {
			'tooltip': true,
			'tooltip--disabled': this.disabled
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
.tooltip {
	background: rgb(13, 13, 102);
	color: white;
	border-radius: 50px;
	padding: 0 20px;
	line-height: 35px;
	border: unset;
    cursor: pointer;
    position: relative;
    display: inline-block;

	&--disabled {
		background: grey;
		pointer-events: none;
	}
}
.tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: black;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 0;
    position: absolute;
    z-index: 1;
    top: 150%;
    left: 50%;
    margin-left: -60px;
}

.tooltip .tooltiptext::after {
    content: "";
    position: absolute;
    bottom: 100%;
    left: 50%;
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    border-color: transparent transparent black transparent;
}

.tooltip:hover .tooltiptext {
    visibility: visible;
}
</style>
