# ms_timeline

## Description
Based on https://github.com/guastallaigor/vue-horizontal-timeline 
"vue-horizontal-timeline": "^0.12.0"  
moved to /components to use content v-html and modification 

MS Timeline displays cards with a title and short content message along a timeline 
determined by items array order. 
load data from an external json file. 
click a card to view itemSelected: data, images, links, pdf
in a panel below the timeline. 

ToDo: fetch items from external data.json file 
put id and date within the same div top, left

## Components
ContentPanel.vue displays scrollable selected content below the timeline 


### Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
