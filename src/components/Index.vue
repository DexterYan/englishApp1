<template>
  <q-layout>
    <div slot="header" class="toolbar primary">
      <q-autocomplete v-model="names" @search="search" @selected="selected" :min-characters="2" :delay="0">
        <q-search placeholder="Name" v-model="names" class="input"/>
      </q-autocomplete>
    </div>
    <div class="layout-view home">
      <div class="layout-padding">
        <div class="grid-rows">
          <div class="wod">
            <div class="row">
              <div class="width-2of3"><div>Word of the Day</div></div>
              <div class="offset-1of3 width-1of3 date"><div class="date">May 27</div></div>
            </div>
            <div class="row">
              <h3 class="word">
                Dexter
              </h3>
            </div>
            <div class="row">
              <div class="meaning">
                dyer, right-handed
              </div>
            </div>
          </div>
          <div class="row gutter wrap justify-stretch content-center news">
            <div class="auto width-1of3"><img src="http://www.rrq.gouv.qc.ca/SiteCollectionDocuments/SiteMobileRRQ/banque-prenoms/fb_banque_prenoms.jpg"></div>
            <div class="auto width-2of3 des"><div class="row">Blog</div><div class="row title">How To Choose An English Name</div></div>
          </div>
          <div class="row gutter wrap justify-stretch content-center news">
            <div class="auto width-1of3"><img src="http://www.rrq.gouv.qc.ca/SiteCollectionDocuments/SiteMobileRRQ/banque-prenoms/fb_banque_prenoms.jpg"></div>
            <div class="auto width-2of3 des"><div class="row">Blog</div><div class="row title">How To Choose An English Name</div></div>
          </div>
          <div class="act_button">
            <div class="row button_item">
              <button class="light-blue raised full-width big">Find your perfect english name</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </q-layout>
</template>

<script>
import Datastore from 'nedb'
import { Utils } from 'quasar'

var db = new Datastore({filename: 'englishname', autoload: true})
function parseNames (names) {
  return names.map(name => {
    let gender = (name.gender === 'F' ? '<div class="search_des">female</div>' : '<div class="search_des">male</div>')
    let genderText = (name.gender === 'F' ? 'female' : 'male')
    return {
      label: '<div class="search_res">' + name.name + '</div>' + gender,
      value: name.name + '/' + genderText
    }
  })
}

export default {
  data () {
    return {
      names: '',
      namelist: parseNames(['dexter'])
    }
  },
  created: () => {
    db.count({}, (_, count) => {
      if (count <= 0) {
        var englishnameDb = require('../assets/englishname.json')
        db.insert(englishnameDb, (err, newDoc) => {
          console.log(err)
        })
      }
    })
  },
  methods: {
    search (names, done) {
      db.find({}, (_, docs) => {
        let nameList = docs.map((v, _) => {
          return {
            name: v.name,
            gender: v.gender
          }
        })
        setTimeout(() => {
          done(Utils.filter(names, {field: 'value', list: parseNames(nameList)}))
        }, 500)
      })
    },
    selected (item) {
      console.log(item)
      this.$router.push(`details/${item.value}`)
    }
  }
}

</script>

<style lang="stylus">
.layout-header
  border-bottom 0px

.search_des
  display inline
  color gray
  margin-left 10px

.search_res
  text-transform capitalize
  display inline
  font-size 20px

.wod
  padding 16px
  margin-bottom 50px
  color ghostwhite
  .date
    float right
  .word
    padding-top 20px
    margin 0 auto
  .meaning
    padding-top 10px
    margin 0 auto

.news
  padding 0 10px 0 10px
  .title
    margin-top 10px
  .des
    color ghostwhite
    margin-left -1rem
  img
    width 70px
    height 70px

.act_button
  margin-top 66px
  .row
    margin-top 10px

.toolbar
  &.primary
    background #7F67D3
    span
      width 100%

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
