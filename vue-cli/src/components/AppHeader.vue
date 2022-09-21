<template>
  <div>
    <h1>{{ propsdata }}</h1>
    <button @click="sendEvent">send</button>
  </div>
</template>
<script>
export default {
  components: {},
  data() {
    return {
      str: "Header",
      emitData: 100,
    };
  },
  props: ["propsdata"],
  setup() {},
  created() {},
  mounted() {},
  unmounted() {},
  methods: {
    sendEvent: function () {
      this.$emit("renew", this.emitData);
    },
  },
};
</script>
