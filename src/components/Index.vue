<template>
  <q-layout>
    <div slot="header" class="toolbar primary">
      <q-search placeholder="Name" class="input" id="dd"/>
    </div>
    <div class="layout-view home">
    </div>
  </q-layout>
</template>

<script>
</script>

<style lang="stylus">
.layout-header
  border-bottom 0px

.toolbar
  &.primary
    background #7F67D3

.input
    background #7F67D3
    .q-search-input
      color white
    .q-search-icon
      color #FFF

.home
  background-image url('~assets/background.jpg')
  background-size 100% 100%
</style>
