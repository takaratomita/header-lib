<template>
  <div
    :class="[
      'header-mod',
      state.active.menuStyle === 'vertical' ? 'vertical' : '',
      state.active.humberger ? 'humberger-menu' : '',
    ]"
  >
    <input
      type="checkbox"
      name="humberger"
      id="humberger"
      v-if="state.active.humberger"
    />
    <label for="humberger" class="humberger" v-if="state.active.humberger">
      <span></span>
      <span></span>
      <span></span>
    </label>
    <div
      :class="[
        'header-mod--inner',
        state.active.menuStyle === 'vertical' ? 'vertical' : '',
      ]"
    >
      <h1 class="header-logo" v-if="state.active.logo">
        <img alt="Vue logo" :src="state.active.logo" />
        <span v-resize="switchByWidth()"></span>
      </h1>
      <nav class="g-nav">
        <ul :class="{ 'gnav-list': true, hov: state.active.menuHover }">
          <li
            v-for="menu in state.menus"
            :key="menu.name"
            :class="{
              'vetical-line': state.active.verticalLine,
              current: isCurrent(menu.class),
            }"
          >
            <a :href="menu.link" v-if="menu.isAnother" target="_blank">{{
              menu.name
            }}</a>
            <a :href="menu.link" v-if="!menu.isAnother">{{ menu.name }}</a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from "vue";

export default defineComponent({
  name: "HelloWorld",
  props: {
    msg: String,
  },
  setup() {
    const state = reactive({
      default: {},
      width: window.innerWidth,
      // @ts-ignore
      ...headerOptions,
    });

    const switchByWidth = () => {
      state.width = window.innerWidth;
      state.default = state.active;

      if (state.mq[0] == "min") {
        if (state.mq[1] < state.width) {
          state.default = state.active;
          state.active = state.mq[2];
          fillFalse();
        }
      } else {
        if (state.width < state.mq[1]) {
          state.active = state.mq[2];
          fillFalse();
        }
      }
    };

    const fillFalse = () => {
      const options = [
        state.menus,
        state.active.humberger,
        state.active.menuStyle,
        state.active.logo,
        state.active.verticalLine,
        state.active.menuHover,
        state.active.width,
        state.mq,
      ];
      for (let i = 0; i < options.length; i++) {
        if (
          options[i] === "" ||
          options[i] === null ||
          options[i] === undefined
        ) {
          options[i] = false;
        } else {
          continue;
        }
      }
    };

    const isCurrent = (cls: string) => {
      const body = document.getElementById("body");

      if (body?.classList.contains(cls)) {
        return true;
      }

      return false;
    };

    fillFalse();
    window.addEventListener("resize", switchByWidth);

    return {
      state,
      switchByWidth,
      isCurrent,
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
  &.vetical-line {
    border-left: 1px solid lightblue;
    &:first-of-type {
      border-left: none;
    }
  }
}
a {
  color: #050505;
  text-decoration: none;
}
.header-mod {
  width: 100%;
  height: auto;
  position: absolute;
  top: 10px;
  left: 50%;
  transform: translateX(-50%);
  box-shadow: rgba(142, 142, 142, 0.19) 0px 6px 15px 0px;
  -webkit-box-shadow: rgba(142, 142, 142, 0.19) 0px 6px 15px 0px;
  color: rgba(255, 255, 255, 0.75);
  &.vertical {
    border: unset;
    box-shadow: unset;
    width: auto;
    height: 100vh;
    left: 20px;
    transform: unset;
  }
  &--inner {
    display: flex;
    align-items: center;
    justify-content: space-around;
    &.vertical {
      flex-direction: column;
      .g-nav {
        background-color: rgba(255, 255, 255, 0.25);
        padding: 0 30px;
        backdrop-filter: blur(6px);
        -webkit-backdrop-filter: blur(6px);
        height: 100vh;
      }
      .gnav-list {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        text-align: left;
        margin-left: 35px;
        .vetical-line {
          border-left: none;
        }
        li {
          padding: 20px 0;
        }
      }
    }
  }
  .header-logo {
    margin: 0;
    img {
      width: 70px;
    }
  }
  .gnav-list {
    li {
      padding: 10px 20px;
      margin: 0 5px;
    }
    a {
      display: block;
    }
    &.hov {
      li {
        position: relative;
        &::after {
          content: "";
          position: absolute;
          background: #1872cc;
          width: 100%;
          bottom: -10px;
          left: 0;
          height: 0;
          transition: height 0.2s ease;
        }
        &:hover::after,
        &.current::after {
          height: 3px;
        }
      }
    }
  }
}

.header-mod {
  &.humberger-menu .header-mod--inner {
    position: relative;
    left: -100vw;
    transition: left 0.3s ease;
  }
  input[type="checkbox"] {
    position: fixed;
    top: -50vw;
    &:checked {
      ~ .header-mod--inner {
        left: 0 !important;
      }
      ~ .humberger {
        span {
          &:first-child {
            -webkit-transform: translateY(10px) rotate(-315deg);
            transform: translateY(10px) rotate(-315deg);
          }
          &:nth-child(2) {
            opacity: 0;
          }
          &:nth-child(3) {
            -webkit-transform: translateY(-10px) rotate(315deg);
            transform: translateY(-10px) rotate(315deg);
          }
        }
      }
    }
  }
  .humberger {
    display: block;
    position: fixed;
    top: 10px;
    left: 10px;
    width: 30px;
    height: 30px;
    transition: all 0.3s ease;
    cursor: pointer;
    z-index: 3;
    span {
      display: block;
      position: absolute;
      left: 0;
      width: 30px;
      height: 2px;
      border-radius: 4px;
      transition: all 0.3s ease;
      background: #050505;
      &:first-child {
        top: 4px;
      }
      &:nth-child(2) {
        top: 14px;
      }
      &:nth-child(3) {
        bottom: 4px;
      }
    }
  }
}
</style>
