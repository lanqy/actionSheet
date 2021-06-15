# actionSheet
A mini actionSheet base on Vue

```vue
<ActionSheet :show="actionSheet.show"
             :title="'This is title'"
             :maskClosable="actionSheet.maskClosable"
             @click="onActionSheetItemClick"
             @cancel="closeActionSheet">
  <div class="select-list"
       slot="content">
    <div class="item"
         v-for="(item, index) in list"
         @click="clickHandler(item, index)"
         :key="index">
         {{item}}
    </div>
  </div>
</ActionSheet>
```

```js
<script>
export default {
  data () {
    return {
      actionSheet: {
        show: false,
        maskClosable: true,
      },
      list: ["a","b","c"]
    }
  },
  methods: {
    closeActionSheet () {
      this.actionSheet.show = false
    },
    clickHandler(item) {
      console.log(item)
    }
  }
}
</script>
```
