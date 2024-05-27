<template>
<BarBottom  class="bg-sky-200" v-bind:title="$slidev.configs.title">
  <Item text="klef-project/recture">
    <carbon:logo-github />
  </Item>
  <Item text="Klef Project">
  </Item>
  <Item text=""># {{ $slidev.nav.currentPage}}</Item>
</BarBottom>
</template>