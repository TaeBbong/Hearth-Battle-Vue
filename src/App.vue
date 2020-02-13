<template>
  <div id="app">
    <HomeHeader></HomeHeader>
    <HomeInput></HomeInput>
    <HomeResult></HomeResult>
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
</style>
