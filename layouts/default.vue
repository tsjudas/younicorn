<template>
  <div>
    <nav class="navbar is-dark is-fixed-top" role="navigation" aria-label="main navigation">
      <div class="navbar-brand flex-row center width-100">
        <a href="/"><p class="logo-txt white">YouNicorn</p></a>
      </div>
    </nav>
    <main>
      <div class="spacer-height-medium"></div>
      <nuxt/>
    </main>
  </div>
</template>

<style>
html * {
  font-family: "Noto Sans JP", sans-serif;
}
.flex-row {
  display: flex;
}
.flex-column {
  display: flex;
  flex-flow: column;
}
.center {
  justify-content: center;
  align-items: center;
}
.flex-start {
  justify-content: flex-start;
  align-items: center;
}
.flex-end {
  justify-content: flex-end;
  align-items: center;
}
.space-evenly {
  justify-content: space-evenly;
  align-items: center;
}
.width-100 {
  width: 100%;
}
.width-96 {
  width: 96%;
}
.width-90 {
  width: 90%;
}
.width-80 {
  width: 80%;
}
.height-100 {
  height: 100%;
}
.spacer-width-small {
  width: 4px;
  height: 100%;
}
.spacer-width-medium {
  width: 12px;
  height: 100%;
}
.spacer-width-large {
  width: 20px;
  height: 100%;
}
.spacer-width-tall {
  width: 48px;
  height: 100%;
}
.spacer-width-huge {
  width: 128px;
  height: 100%;
}
.spacer-height-small {
  width: 100%;
  height: 4px;
}
.spacer-height-medium {
  width: 100%;
  height: 12px;
}
.spacer-height-large {
  width: 100%;
  height: 20px;
}
.spacer-height-tall {
  width: 100%;
  height: 48px;
}
.spacer-height-huge {
  width: 100%;
  height: 128px;
}
.bold {
  font-weight: bold;
}
.white {
  color: white;
}
.black {
  color: black;
}
.cursor {
  cursor: pointer;
}
</style>

<style scoped>
.logo-txt {
  font-size: 24px;
}
</style>

<script>
export default {
  head() {
    return {
      htmlAttrs: {
        class: 'has-navbar-fixed-top'
      }
    }
  }
}
</script>
