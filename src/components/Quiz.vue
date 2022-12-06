<template>
  <div class="container">
    <h1>The Windows ME operating system was released in the year 2000."</h1>

    <input type="radio" name="options" value="True" />
    <label>True</label>
    <br />

    <input type="radio" name="options" value="True" />
    <label>False</label>
    <br />

    <button class="send" type="button">Send</button>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style lang="scss">
.container {
  text-align: center;
  max-width: 960px;
  margin: 60px auto;

  input[type="radio"] {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #FFF;
    background-color: #1867C0;
    border: 1px solid #1867C0;
    cursor: pointer;
  }
}
</style>
