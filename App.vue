<template>
	<div>
		<form v-show="showForm" action @submit.prevent="showForm = false">
			<textarea v-model="text"></textarea><br><br>
			<button type="submit">Show Flash Card</button>
		</form>
		<div v-show="!showForm">
            <div class="buttons">
                <a href @click.prevent="showForm = true" class="back">Back</a>
                <a href @click.prevent="toggle = !toggle">Toggle</a><br>
            </div>
			<div class="note">Press Space to Toggle</div>
			<p>{{ content }}</p>
		</div>
    </div>
</template>

<style>
    .buttons{text-align: right;}
	.note{text-align: left; margin-top:-5px; font-size:11px; color:#9f9f9f}
    a,button{
        background-color: #4CAF50; /* Green */
        border: none;
        color: white;
        padding: 15px 32px;
        text-align: center;
        text-decoration: none;
        display: inline-block;
        font-size: 16px;
        margin:5px;
    }
    a.back{background-color: rgba(32, 105, 191, 0.29)
    }
	p {
		font-size: 18px;
	}

	textarea {
		width: 400px;
		max-width: 100%;
		height: 200px;
		border:1px solid black;
	}
</style>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({

	data() {
		return {
			text: '',
			showForm: true,
			toggle: false,
		};
	},

	computed: {
		content() {
			if (this.toggle) {
				return this.text.split(' ').map(word => this.parseWord(word)).join(' ');
			}

			return this.text;
		},

	},

    mounted() {
	    document.addEventListener('keyup', (e) => {
	        if (!this.showForm && (e.which === 32 || e.code === 'Space')) {
	            this.toggle = !this.toggle;
            }

        });
    },

	methods: {

		parseWord(word) {
			if (!word || !word.length <= 1) return word;

			let text = word[ 0 ];
			let leftover = word.toString().substr(1);
			let regex = /([a-zA-Z])/gi;
			text = text + leftover.replace(regex, '');

			return text;
		}
	}
});
</script>

<style lang="scss" scoped>
	.container {
		color: green;
	}
</style>
