<template>
  <div>
    <app-header :propsdata="str" @renew="renewString"></app-header>{{ str }}
  </div>
</template>
<script>
import AppHeader from "./components/AppHeader.vue";
export default {
  components: { AppHeader },
  data() {
    return {
      str: "hi",
    };
  },

  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    renewString: function (value) {
      this.str = "hello";
      console.log(value);
    },
  },
};
</script>
