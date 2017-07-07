<template>
  <q-layout>
    <div slot="header" class="toolbar primary">
      <q-autocomplete v-model="names" @search="search" :delay="0">
        <q-search placeholder="Name" v-model="names" class="input"/>
      </q-autocomplete>
    </div>
    <div class="layout-view details">
      <div class="header">
        <div class="intro">
          <avatar username="Dexter" :size="100" class="avatar-name"></avatar>
          <div class="name">Dexter</div>
        </div>
      </div>
      <div class="sub-intro">
        <div class="left-block">Good</div>
        <div class="right-block"></div>
      </div>
    </div>
  </q-layout>
</template>

<script>
// import Datastore from 'nedb'
import {Utils} from 'quasar'
import Avatar from 'vue-avatar/dist/Avatar'

function parseNames () {
  var names = ['dexter', 'sally']
  return names.map(name => {
    return {
      label: name,
      value: name
    }
  })
}

export default {
  components: {
    Avatar
  },
  data () {
    return {
      names: '',
      namelist: parseNames()
    }
  },
  created: () => {
    // let db = new Datastore({filename: 'englishname', autoload: true})
  },
  methods: {
    search (names, done) {
      setTimeout(() => {
        done(Utils.filter(names, {field: 'value', list: parseNames()}))
      }, 500)
    }
  }
}

</script>

<style lang="stylus">
.layout-header
  border-bottom 0px

.toolbar
  &.primary
    background #7F67D3
    span
      width 100%

.details
  .header
    background-image url('~assets/blue_background.png')
    background-size 100% 100%
    width 100%
    height 36%
    .intro
      padding-top 18%
      padding-left 10%
      .avatar-name 
        display inline-block 
      .name
        display inline-block
        font-weight 300
        font-size 3em
        color white
        margin-left 12%
  .sub-intro
    height 50%
    .left-block
      float left
      width 50%
      height 40%
      background-color #26abff
    .right-block
      float right
      width 50%
      height 40%
      background-color #ff7793
</style>
