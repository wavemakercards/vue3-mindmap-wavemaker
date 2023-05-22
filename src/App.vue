<template>
  <div class="container">
    <mindmap class="left-bottom" v-model="MMdata" :branch="options.branch" :x-gap="options.xgap" :y-gap="options.ygap"
      :zoom="options.zoom" :fit-btn="options.fitbtn" :center-btn="options.centerbtn" :download-btn="options.downloadbtn"
      :drag="options.drag" :edit="options.edit" :add-node-btn="options.addnodebtn" :sharp-corner="options.sharpcorner"
      :ctm="options.contextmenu" :timetravel="options.timetravel" @update:model-value="onChange"
      :contextText="contextText" @handleEmit="dostuff" :key="updateKey" />
  </div>
  <div class="inputform">
    <div v-if="updateObj">

      <input type="text" v-model="updateObj.name" />
      <textarea v-model="updateObj.info"></textarea>
      <hr />
      <button @click="doUpdate">Save</button>
    </div>
  </div>
</template>

<script>
import learn from './learn.json'
import contextLang from './contextLang.json'
import Mindmap from './components/Mindmap'

export default {
  name: 'App',
  components: {
    Mindmap
  },
  data() {
    return {
      MMdata: learn,
      contextText: contextLang,
      lang: "en",
      updateKey: 1,
      updateObj: null,
      options: {
        branch: 4,
        xgap: 84,
        ygap: 18,
        centerbtn: true,
        fitbtn: true,
        timetravel: true,
        downloadbtn: true,
        addnodebtn: true,
        keyboard: false,
        zoom: true,
        drag: true,
        edit: true,
        contextmenu: true,
        sharpcorner: false,
        vertical: false,
      }
    }
  },
  methods: {
    doUpdate() {
      this.updateKey++
    },
    dostuff(v) {
      console.log("dostuff")
      if (!v) {
        this.updateObj = v
        console.log("nulled")
        return false
      }
      //this.MMdata[0].name = "boom"
      let arr = v.id.split("-")
      let tObj = this.MMdata

      arr.forEach((i, l) => {
        if (arr.length === l + 1) {
          tObj = tObj[i]
        } else {
          tObj = tObj[i].children
        }
        console.log(tObj)
        this.updateObj = tObj
      })
    },
    onChange() {
      console.log("Change", this.MMdata)
    }
  }
}
</script>

<style >
body {
  background-color: #efefef;
}

.inputform {
  position: absolute;
  top: 0px;
  right: 0px;
  bottom: 0px;
  width: 320px;
  background-color: black;
}

.container {
  position: absolute;
  top: 0px;
  left: 0px;
  bottom: 0px;
  right: 320px;
}
</style>
