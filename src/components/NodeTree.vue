<template>
  <li>
    <label
      class="tree__label"
      @click="handleClick(node)"
      :class="[
        hasChildren && expanded ? 'childItem' : 'childLast',
        hasChildren ? 'iconChild' : '',
        expanded ? 'active' : '',
      ]"
    >
      <span v-if="hasChildren" class="list-icon"
        ><span class="icon-up" v-if="expanded">{{ "&#9698;" }}</span
        ><span class="icon-down" v-else>{{ "&#9700;" }}</span></span
      >
      <span class="list-index">{{ indexNode }}</span
      ><span class="list-title">{{ node.label }}</span></label
    >
    <ul v-if="node.children && node.children.length">
      <NodeTree
        v-show="expanded"
        v-for="child in node.children"
        :indexNode="indexNode + 1"
        :key="child"
        :node="child"
      >
      </NodeTree>
    </ul>
  </li>
</template>

<script>
export default {
  name: "NodeTree",

  props: {
    node: Object,
    indexNode: Number,
  },

  data() {
    return {
      expanded: false,
      listParent: [],
    };
  },
  computed: {
    hasChildren() {
      return this.node.children;
    },
  },
  watch: {},
  methods: {
    handleClick(node) {
      this.expanded = !this.expanded;
      this.$emit("getNode", node);
    },
  },
};
</script>

<style lang="scss">
body {
  margin: 30px;
  font-family: sans-serif;
}

/* ————————————————————–
  Tree core styles
*/
.tree {
  margin: 1em;
  /* ————————————————————–
  Tree rows
*/
  & li {
    line-height: 1.2;
    position: relative;
    padding: 0 0 1em 1em;
  }
  & ul li {
    padding: 1em 0 0 1em;
  }
  & > li:last-child {
    padding-bottom: 0;
  }
  /* ————————————————————–
  Tree labels
*/
  &__label {
    position: relative;
    display: inline-block;
    background: #fff;
  }

  &__label {
    cursor: pointer;
  }

  &__label:hover {
    color: #666;
  }
  & li:before {
    position: absolute;
    top: 0;
    bottom: 0;
    left: -0.5em;
    display: block;
    width: 0;
    border-left: 1px solid #777;
    content: "";
  }
  &__label:after {
    position: absolute;
    top: 0;
    left: -24.5px;
    display: block;
    height: 0.5em;
    width: 1em;
    content: "";
    border-bottom: 0;
    border-bottom: 0;
    border-left: 0;
    bottom: 0;
    top: 0.5em;
    height: auto;
  }
  & li:last-child:before {
    height: 1.5em;
    bottom: auto;
  }

  & > li:last-child:before {
    display: none;
  }
}

.childItem.tree__label:after {
  border-radius: 0 0 0 0;
  border-top: 1px solid #777;
  border-right: 1px solid #777;
}

.childLast.tree__label:after {
  position: absolute;
  top: -1px;
  left: -1.5em;

  height: 0.5em;
  width: 5px;
  border-bottom: 1px solid #777;

  border-radius: 0 0 0 0 0;
}

.list {
  &-index {
    background: #51529b;
    color: white;
    font-size: 12px;
    margin-right: 5px;
    padding: 1px 5px;
    border-radius: 4px;
    position: absolute;
    left: -16px;
    z-index: 2;
  }
  &-title {
    margin-left: 4px;
  }
  &-icon {
    position: absolute;
    font-size: 10px;
  }
}
.icon {
  &-down {
    position: absolute;
    left: -26px;
    top: 4px;
    z-index: 1;
  }
  &-up {
    position: absolute;
    left: -29px;
    top: 0px;
    z-index: 2;
  }
}
.select{
  &__box {
  width: 512px;
  margin: auto;
}
&__control {
  display: flex;
  border-radius: 5px;
  box-shadow: 0px 0px 3px 0px #007bc3;
  border: 1px solid transparent;
  align-items: center;
}
&__input {
  flex: 1;
  outline: none;
  border: none;
  font-size: 16px;
  padding: 15px 10px 15px 18px;
  border-radius: 10px;
}
&__icon {
  padding: 5px 10px;
  font-size: 20px;
  cursor: pointer;
}
&__icon:hover {
  opacity: 0.5;
}

}




</style>
