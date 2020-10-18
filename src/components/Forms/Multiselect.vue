<template>
  <div class="form-container">
    <span class="name">{{ name }}</span>
    <div class="pseudo-box" @click="toggleList">
      <span
        class="selected-item"
        v-for="(o, i) in value"
        :key="i"
        @click="removeItem(o)"
        >{{ o }}</span
      >
    </div>
    <div class="popup" :class="{ disabled: !isPopupActive }">
      <div
        class="item"
        v-for="(o, i) in options"
        :key="i"
        :class="{ selected: value.includes(o) }"
        @click="addItem(o)"
      >
        <span>{{ o }}</span>
      </div>
    </div>
    <span class="error">{{ error }}</span>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    options: Array,
    value: Array,
    error: String,
  },
  data: () => ({
    isPopupActive: false,
  }),
  methods: {
    toggleList() {
      this.isPopupActive = !this.isPopupActive;
    },
    addItem(item) {
      if (this.value.includes(item)) {
        this.removeItem(item);
        return;
      }
      this.value.push(item);
    },
    removeItem(item) {
      this.value.map((v, i) => {
        if (item == v) this.value.splice(i, 1);
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.popup {
  position: absolute;
  width: 100%;
  min-height: 30px;
  max-height: 90px;

  overflow: scroll;

  top: 55px;
  z-index: 9999;

  background-color: white;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.25);

  .item {
    position: relative;

    height: 30px;
    width: 100%;

    display: flex;
    align-items: center;
    padding: 0px 5px;
    box-sizing: border-box;

    background-color: #e0e0e0;

    span {
      font-size: 12px;
    }
  }
}

.disabled {
  visibility: collapse;
}

.selected {
  background-color: rgb(121, 231, 171) !important;
}

@media screen and (max-width: 375px) {
  .popup {
    top: 50px;
  }
}
.pseudo-box {
  position: relative;
  background: #ffffff;
  border: 1px solid #c1c1c1;
  box-sizing: border-box;
  border-radius: 6px;
  height: 30px;
  padding: 2px 5px;
  outline: none;
  width: 100%;
  color: #4c4c4c;

  display: flex;
  flex-direction: row;
  justify-content: flex-start;
  align-items: center;
  //   overflow: hidden;
}
.selected-item {
  position: relative;

  height: 60%;
  padding: 2px 5px;

  margin-right: 5px;
  border-radius: 5px;

  color: black;
  font-size: 10px;
  font-weight: bold;

  background-color: #95e0e6;
}
</style>