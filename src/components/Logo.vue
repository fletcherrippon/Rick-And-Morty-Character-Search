<template>
  <div>
    <h1 class="logo">
      <div class="heading">Rick <span class="sub-heading">And</span> Morty</div>
      <span class="sub-heading">Character Search</span>
    </h1>
  </div>
</template>

<script>
  export default {
    name: 'Logo'
  }
</script>

<style>
  .logo {
    margin: 0;
    color: #91faff;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    -webkit-text-stroke: .1px #003852;
  }

  .sub-heading {
    font-size: 18px;
    font-family: "Get Schwifty";
  }
  .heading {
    font-size: 34px;
    font-family: "Get Schwifty";
  }

  .logo span {
    margin-top: 8px;
  }
</style>