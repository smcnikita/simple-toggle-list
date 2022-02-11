<template>
	<div class="hello">
		<div class="list-toggle">
			<table
					class="list-toggle__wrapper"
					:class="{'wrapper-toggle__close': !isOpen, 'wrapper-toggle__open': isOpen}"
			>
				<tbody>
				<tr class="wrapper-vertical-middle">
					<td style="width: 5%;">
						<svg
								@click="isOpen = !isOpen"
								xmlns="http://www.w3.org/2000/svg"
								class="wrapper-chevron"
								viewBox="0 0 16 16"
								:style="fill"
								:class="{'wrapper-chevron__open': isOpen}"
						>
							<path fill-rule="evenodd"
										d="M1.646 4.646a.5.5 0 0 1 .708 0L8 10.293l5.646-5.647a.5.5 0 0 1 .708.708l-6 6a.5.5 0 0 1-.708 0l-6-6a.5.5 0 0 1 0-.708z" />
						</svg>
					</td>
					<td>
						<span class="wrapper-title">{{ title }}</span>
					</td>
				</tr>
				</tbody>
			</table>
			<div
					class="list-toggle__body body-toggle__close"
					:class="{'body-toggle__open': isOpen, 'body-toggle__close': !isOpen}"
			>
				<slot />
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'ToggleComponent',
	emits: [ 'open' ],
	props: {
		open: {
			type: Boolean,
			required: false,
			default: false,
		},
		fillArrow: {
			type: String,
			required: false,
			default: 'currentColor',
		},
		title: {
			type: String,
			required: true,
		}
	},
	computed: {
		fill() {
			return 'fill:' + this.fillArrow + ';';
		}
	},

	data() {
		return {
			isOpen: this.open,
		};
	},

	watch: {
		isOpen(newValue) {
			this.$emit('open', newValue);
		}
	}
};
</script>

<style scoped>
.hello {
	max-width: 700px;
	margin: 0 auto;
}

.wrapper-vertical-middle {
	vertical-align: middle;
}

.list-toggle__wrapper {
	width: 100%;
	padding-bottom: 5px;
}

.wrapper-toggle__close {
	border-bottom: 1px solid #D1D1D1;
}

.wrapper-toggle__open {
	border-bottom: none;
}

.wrapper-chevron {
	width: 18px;
	height: 18px;
	cursor: pointer;
	transform: rotate(-90deg);
	border-radius: 3px;
	padding: 5px;
	transition: transform linear 0.3s;
}

.wrapper-chevron:hover {
	background-color: #EFEFEF;
}

.wrapper-chevron__open {
	transform: rotate(0deg);
	transition: transform linear 0.3s;
}

.wrapper-title {
	text-align: left;
}

.list-toggle__body {
	width: 100%;
	max-height: 200px;
	overflow: auto;
	border: 1px solid #D1D1D1;
	border-radius: 3px;
	padding: 15px;
}

.body-toggle__close {
	display: none;
}

.body-toggle__open {
	display: block;
}
</style>
