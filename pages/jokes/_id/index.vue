<template>
  <div>
    <nuxt-link to="/jokes">Back</nuxt-link>
    <p>{{joke}}</p>
    <hr>
    <p>
      <small>Joke ID: {{$route.params.id}}</small>
    </p>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      joke: {}
    };
  },
  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };

    try {
      const res = await axios.get(
        `https://icanhazdadjoke.com/j/${this.$route.params.id}`,
        config
      );
      this.joke = res.data.joke;
    } catch (err) {
      console.log(err);
    }
  },
  head() {
    return {
      title: this.joke,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "jokes index"
        }
      ]
    };
  }
};
</script>

<style></style>