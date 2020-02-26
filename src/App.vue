<template>
  <div id="app">
    <HomeHeader></HomeHeader>
    <HomeInput></HomeInput>
    <HomeMore></HomeMore>
    <HomeFooter></HomeFooter>
  </div>
</template>

<script>
import HomeHeader from "./components/HomeHeader";
import HomeInput from "./components/HomeInput";
import HomeResult from "./components/HomeResult";
import HomeMore from "./components/HomeMore";
import HomeFooter from "./components/HomeFooter";

export default {
  components: {
    HomeHeader: HomeHeader,
    HomeInput: HomeInput,
    HomeResult: HomeResult,
    HomeMore: HomeMore,
    HomeFooter: HomeFooter
  }
};
</script>

<style>
body {
  text-align: center;
  background-color: #f6f6f8;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}
.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  width: 300px;
}
</style>
