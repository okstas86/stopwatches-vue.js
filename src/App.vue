<template>
  <StopwatchDisplay></StopwatchDisplay>
  <TestForm2></TestForm2>
</template>
<script>
import StopwatchDisplay from "./components/StopwatchDisplay.vue";

export default {
  components: { StopwatchDisplay },
};
</script>
<style>
@font-face {
  font-family: "Gotham Pro Black";
  src: url("./assets/fonts/gothampro.ttf") format("truetype");
}

body {
  font-family: "Gotham Pro Black", sans-serif;
  background-color: #353638;
}
#app {
  flex-direction: row;
  justify-content: flex-start;
  align-items: flex-start;
}
</style>
