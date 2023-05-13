# vue3-mindmap

[![npm](https://img.shields.io/npm/v/vue3-mindmap)](https://www.npmjs.com/package/vue3-mindmap)
[![build](https://github.com/hellowuxin/vue3-mindmap/actions/workflows/blank.yml/badge.svg)](https://github.com/hellowuxin/vue3-mindmap/actions)
[![coveralls](https://img.shields.io/coveralls/github/hellowuxin/vue3-mindmap)](https://coveralls.io/github/hellowuxin/vue3-mindmap)

> Mindmap component for Vue3 inspired by [MindNode](https://mindnode.com)

[live demo / demo page](https://5xin.xyz/vue3-mindmap)  
[Directory Description / Directory Description](./Directory.md)

## Install

```sh
npm install vue3-mindmap
```

## PROPS

| Name         | Type                     | Default    | Description          |
| ---          | ---                      | ---        | ---                  |
| v-model | Data[] | undefined | set mind map data |
| x-gap | Number | 84 | Set horizontal gap between nodes |
| y-gap | Number | 18 | Set vertical gap between nodes |
| branch | Number | 4 | set the line width |
| scale-extent | [Number, Number] | [0.1, 0.8] | set zoom extent |
| timetravel | Boolean | false | whether to display undo redo button |
| drag | Boolean | false | Set whether the node can be dragged |
| zoom | Boolean | false | Can zoom and drag |
| edit | Boolean | false | whether editable |
| center-btn | Boolean | false | Whether to display the center button |
| fit-btn | Boolean | false | Whether to show the zoom button |
| add-node-btn | Boolean | false | Whether to display the add node button |
| download-btn | Boolean | false | Whether to display the download button |
| sharp-corner | Boolean | false | set the corners to be rounded or straight |
| ctm | Boolean | false | Whether to respond to the right-click menu |
| local | 'zh' \| 'en' \| 'ptBR' | 'zh' | i18n |

Added contextTxt prop that provides the text for the context menu so you can handle language changes yourself
Just provide this with your altered text to the mindmap and it will be passed down to the context menu

```js
contextTxt = {
    "collapse": "Collapse this node",
    "expand": "Expand from here",
    "delete": "Delete Node",
    "delete-one": "Delete a single node",
    "add": "Add Child node",
    "add-parent": "Add Parent node",
    "add-sibling": "Add Sibling node",
    "add-sibling-before": "Add Sibling node before",
    "cut": "Cut",
    "copy": "Copy",
    "paste": "Paste",
    "selectall": "Select all",
    "zoomin": "Zoom in",
    "zoomout": "Zoom out",
    "zoomfit": "Zoom fit"
}

```

## Example

```html
<template>
  <mindmap v-model="data"></mindmap>
</template>

<script>
import mindmap from 'vue3-mindmap'
import 'vue3-mindmap/dist/style.css'

export default defineComponent({
  components: { mindmap },
  setup () => {
    const data = [{
      "name": "How to learn D3",
      "children": [
        {
          "name": "preliminary knowledge",
          "children": [
            { "name":"HTML & CSS" },
            { "name":"JavaScript" },
            ...
          ]
        },
        {
          "name": "installation",
          "collapse": true,
          "children": [ { "name": "folded node" } ]
        },
        { "name":"进阶", "left": true },
        ...
      ]
    }]

    return { data }
  }
})
</script>
```

## Notice

- When xGap is less than a certain value, the trigger of the parent node may block the trigger of the child node due to the existence of the add button, and cannot respond to the click of the child node

## to be solved

- right angle branch radius

## All

- Multi-select nodes
- Multi-master nodes
- More node styles