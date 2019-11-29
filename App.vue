<template>
<div>
    <form v-show="showForm" action @submit.prevent="showForm = false">
    <textarea v-model="text"></textarea><br><br>
    <button type="submit">Show Flash Card</button>
    </form>
    <div v-show="!showForm">
        <a href @click.prevent="showForm = true">Back</a><br>
        <a href @click.prevent="toggle = !toggle">Toggle</a><br>
        <p>{{ content }}</p>
    </div>
</template>

<style>
p { font-size: 18px; }
textarea{ min-width: 400px; min-height: 200px; }
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

    methods: {

        parseWord(word) {
            let text = word[0];
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