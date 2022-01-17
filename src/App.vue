<template>
  <div class="container">
    <div class="container__left-container left-container">
      <ul class="left-container__lists">
        <li v-for="(list, indexList) in lists" :key="indexList">
          <div
            class="left-container__caret-ic"
            @click="caretShowList(indexList)"
            v-bind:class="{ leftContainerCaretIc_act: list.caretShow }"
          >
            <i class="fas fa-angle-right"></i>
          </div>
          <label>
            <input
              type="checkbox"
              v-model="list.state"
              @click="changeCheckboxList(indexList)"
            />{{ ` List ${indexList + 1}` }}
          </label>
          <ul v-show="list.caretShow" class="left-container__items lists-items">
            <li
              v-for="(item, indexItem) in lists[indexList]"
              :key="item.count"
              class="lists-items__item"
            >
              <div>
                <div class="lists-items__name">
                  <label>
                    <input
                      type="checkbox"
                      v-model="item.state"
                      @click="changeCheckboxIttem(indexList, item)"
                    />{{ ` Item ${indexItem + 1}` }}</label
                  >
                </div>
                <div class="lists-items__params">
                  <input type="number" v-model.number="item.count" />
                  <input type="color" v-model="item.color" />
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
    <div class="container__right-container right-container">
      <ul class="right-container__lists">
        <li v-for="(list, indexList) in lists" :key="indexList">
          <ul class="right-container__items">
            <span>{{ `List ${indexList + 1}` }}</span>
            <li
              v-for="item in lists[indexList]"
              v-bind:key="item.id"
              v-show="item.state"
            >
              <div
                v-for="index in item.count"
                v-bind:key="index.id"
                @click="item.count = index"
                class="visi"
                v-bind:style="{ backgroundColor: item.color }"
              ></div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      lists: [
        [
          { count: 15, color: "#000000", state: false },
          { count: 20, color: "#80ff00", state: false },
          { count: 5, color: "#00ffff", state: false },
          { count: 12, color: "#16a085", state: false },
        ],
        [
          { count: 21, color: "#ff00bf", state: false },
          { count: 17, color: "#8c7373", state: false },
        ],
        [{ count: 41, color: "#ffff00", state: false }],
        [],
      ],
    };
  },
  methods: {
    changeCheckboxList(indexList) {
      for (let item of this.lists[indexList]) {
        item.state = this.lists[indexList].state === true ? false : true;
      }
      if (!this.lists[indexList].caretShow) {
        this.caretShowList(indexList);
      }
    },
    changeCheckboxIttem(indexList, listItem) {
      if (this.lists[indexList].state && listItem.state) {
        this.lists[indexList].state = false;
      } else if (!this.lists[indexList].state) {
        for (let item of this.lists[indexList]) {
          if (item != listItem && !item.state) {
            this.lists[indexList].state = false;
            break;
          } else {
            this.lists[indexList].state = true;
          }
        }
      }
    },
    caretShowList(indexList) {
      this.lists[indexList].caretShow =
        this.lists[indexList].caretShow === true ? false : true;
    },
  },
};
</script>

<style src="./assets/style.css"></style>
