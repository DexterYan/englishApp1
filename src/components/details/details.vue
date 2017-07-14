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
          <div class="meaning">dyer, right-handed</div>
        </div>
      </div>
      <div class="sub-intro">
        <div class="left-block">
          <div class="block-des">Latin</div>
          <div class="block-title">Origin</div>
        </div>
        <div class="right-block">
          <div class="block-des">Male</div>
          <div class="block-title">Gender</div>
        </div>
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
        float left
      .name
        float right
        font-weight 300
        font-size 3em
        margin-right 20%
        color white
      .meaning
        float right
        color #87CEFA
        margin-right 20%
  .sub-intro
    height 50%
    color white
    .left-block
      float left
      width 50%
      height 40%
      background-color #26C1FF
    .right-block
      float right
      width 50%
      height 40%
      background-color #FF96C8
    .block-title
      text-align center
    .block-des
      padding-top 20%
      font-size 28px
      text-align center
</style>
