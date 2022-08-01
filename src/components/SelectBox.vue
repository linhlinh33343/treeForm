<template>
  <div class="select__box">
    <div class="select__control" @click="selectList()">
      <input
        class="select__input"
        type="text"
        placeholder="A cool sub-folder 1"
      />
      <i v-if="isShowTree" class="select__icon fa-solid fa-angle-down" ></i> 
      <i v-else class=" select__icon fa-solid fa-angle-up"></i>
    </div>
    <div v-show="isShowTree" class="province-select">
       <div class="province-list">
      <ul class="tree">
        <node-tree class="item" :node="tree" :indexNode="indexNode"></node-tree>
      </ul>
       </div>
    </div>
  </div>
</template>

<script>
import NodeTree from "./NodeTree.vue";

export default {
  name: "SelectBox",
 
  data: () => ({
    indexNode:1,
    isShowTree:false,
    tree: {
      label: "Root Folder",
      children: [
        {
          id:1,
          label: "A cool sub-folder 1",
          children: [
            {
              id:2,
              label: "A cool sub-sub-folder 1.1",
              children: [

                {id:3,label: "A cool sub-sub-folder 1.1.1" },
                {id:4, label: "A cool sub-sub-folder 1.1.2" },
              ],
            },
            {id:5, label: "A cool sub-sub-folder 1.2" },
          ],
        },
        {
          id:6,
          label: "A cool sub-folder 2",
          children: [
            {id:7, label: "A cool sub-sub-folder 2.1" },
            {id:8, label: "A cool sub-sub-folder 2.2" },
          ],
        },
        {
          id:9,
          label: "A cool sub-folder 3",
          children: [
            {id:10, label: "A cool sub-sub-folder 3.1" },
            {id:11, label: "A cool sub-sub-folder 3.2" },
          ],
        },
      ],
    },
  }),
  components: {
    NodeTree,
    
  },
  methods:{
        selectList(){
           this.isShowTree=!this.isShowTree; 
        }
    }
};
</script>

<style>

.isClick {
  border: 1px solid rgba(160, 160, 228, 0.952);
}

.province-select {
  margin-top: 3px;
  box-shadow: 0 0 10px 0.5px rgb(0 0 0 / 15%);
  border-radius: 4px;
  padding: 16px 20px;

}
.province-list {
  padding-left: 0;
  margin: 0;
  height: calc(var(--heightProvinceList) - var(--heightButton));
  overflow-y: scroll;
  border-radius: 4px;
  max-height: 320px;
}

::-webkit-scrollbar {
  width: 8px;
  height: 62px;
  border-radius: 6px;
}
::-webkit-scrollbar-thumb {
  background: #dcdcdc;
  width: 8px;
  height: 62px;
  border-radius: 6px;
} */

.province-list li {
  text-align: left;
  height: 40px;
  padding-left: 20px;
  display: flex;
  align-items: center;
  cursor: pointer;
}

/* 
li{
    width: 100%;
    cursor: pointer;
}; */

ul {

  text-align: left;
  list-style: none;
  padding: 0;
}


</style>
