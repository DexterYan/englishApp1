<template>
  <q-layout>
    <div slot="header" class="toolbar primary">
      <q-search placeholder="Name" class="input"/>
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

export default {
  created: () => {
    let db = new Datastore({filename: 'englishname', autoload: true})
    db.count({}, (_, count) => {
      if (count <= 0) {
        var englishnameDb = require('../assets/englishname.json')
        db.insert(englishnameDb, (err, newDoc) => {
          console.log(err)
        })
      }
    })
    db.find({ name: 'dexter' }, (err, docs) => {
      console.log(err)
      console.log(docs)
    })
  }
}

</script>

<style lang="stylus">
.layout-header
  border-bottom 0px

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
