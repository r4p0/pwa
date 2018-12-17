<template>
  <div id="app">
    <header class="header">
      <button role="tab" class="header__menu js-toggle-menu" @click="open = true">Toggle nav menu</button>

      <h1 class="header__title">{{ title }}</h1>
    </header>
    <main class="main js-global-main" aria-role="main">
      <router-view/>
    </main>

    <aside class="toast-view js-toast-view"></aside>

    <!-- Loading Dialog For use by Activities -->
    <div class="loader js-global-loader is-hidden">
      <svg viewBox="0 0 32 32" width="32" height="32">
        <circle id="spinner" cx="16" cy="16" r="14" fill="none"></circle>
      </svg>
    </div>

    <section
      v-bind:class="['side-nav', 'js-side-nav', open ? 'side-nav--visible': '']"
      @click="open = false"
    >
      <div
        class="side-nav__content js-side-nav-content side-nav__content--animatable"
        :style="{ 'transform': `translateX(${open ? '0': '-102%'})`}"
      >
        <div class="side-nav__header">
          <h2 class="side-nav__title">{{ title }}</h2>
        </div>

        <div class="side-nav__body">
          <router-link role="tab" tabindex="0" class="side-nav__blog-post" to="./" exact>Home</router-link>
          <router-link role="tab" tabindex="0" class="side-nav__blog-post" to="./about" exact>About</router-link>
          <router-link role="tab" tabindex="0" class="side-nav__blog-post" to="./calc" exact>Calc</router-link>
        </div>
        <div class="side-nav__version">Version @VERSION@</div>
      </div>
    </section>

    <aside class="toast-view js-toast-view"></aside>
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      title: "title",
      open: false
    };
  }
};
</script>

<style>
body {
  display: -ms-flexbox;
}

body,
body:after,
html {
  width: 100%;
  height: 100%;
}

.side-nav:before,
body:after {
  content: "";
}

.side-nav,
html {
  overflow: hidden;
}

*,
.loader #spinner {
  box-sizing: border-box;
}

* {
  -webkit-touch-callout: none; /*系统默认菜单被禁用*/
  -webkit-user-select: none; /*webkit浏览器*/
  -khtml-user-select: none; /*早期浏览器*/
  -moz-user-select: none; /*火狐*/
  -ms-user-select: none; /*IE10*/
  user-select: none;
}

input {
  -webkit-user-select: auto; /*webkit浏览器*/
}

body,
html {
  padding: 0;
  margin: 0;
  font-family: Helvetica, Verdana, sans-serif;
  font-weight: 400;
  font-display: optional;
  color: #444;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  display: -webkit-flex;
  display: flex;
  -webkit-flex-direction: column;
  -ms-flex-direction: column;
  flex-direction: column;
  -webkit-flex-wrap: nowrap;
  -ms-flex-wrap: nowrap;
  flex-wrap: nowrap;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
  -webkit-align-content: stretch;
  -ms-flex-line-pack: stretch;
  align-content: stretch;
  background: #ececec;
}

body:after {
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
  background: #fafafa;
  opacity: 0;
  will-change: opacity;
  transition: opacity 333ms cubic-bezier(0, 0, 0.21, 1) 0.4s;
}

h1,
h2,
h3,
h4,
h5,
h6 {
  font-family: Roboto, Helvetica, Verdana, sans-serif;
}

a {
  color: #ff4081;
}

.is-hidden {
  display: none;
}

button::-moz-focus-inner {
  border: 0;
}

.side-nav:before {
  will-change: opacity;
  width: 100%;
}

.side-nav {
  width: 100%;
  height: 100%;
  position: fixed;
  pointer-events: none;
  top: 0;
  left: 0;
}

.side-nav:before {
  height: 100%;
  background: #000;
  opacity: 0;
  display: block;
  position: absolute;
  transition: opacity 233ms cubic-bezier(0, 0, 0.21, 1);
}

.side-nav--visible {
  pointer-events: auto;
}

.side-nav--visible:before {
  opacity: 0.7;
}

.side-nav__content {
  background: #fafafa;
  width: 304px;
  height: 100%;
  overflow: hidden;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.14), 0 4px 8px rgba(0, 0, 0, 0.28);
  will-change: transform;
  -webkit-transform: translateX(-102%);
  transform: translateX(-102%);
}

.side-nav__content--animatable {
  transition: -webkit-transform 233ms cubic-bezier(0, 0, 0.21, 1);
  transition: transform 233ms cubic-bezier(0, 0, 0.21, 1);
  transition: transform 233ms cubic-bezier(0, 0, 0.21, 1),
    -webkit-transform 233ms cubic-bezier(0, 0, 0.21, 1);
}

.side-nav__header {
  background: url(./assets/side-nav-bg@2x.jpg) #3f51b5;
  background-size: cover;
  width: 100%;
  height: 171px;
  position: relative;
}

.side-nav__title {
  font-size: 16px;
  line-height: 1;
  color: #fff;
  position: absolute;
  bottom: 8px;
  left: 16px;
  height: 16px;
  font-weight: 500;
}

.side-nav__body {
  padding-top: 8px;
}

.side-nav__version {
  position: absolute;
  bottom: 16px;
  right: 16px;
  font-size: 14px;
  opacity: 0.54;
}

.side-nav__blog-post,
.side-nav__delete-all,
.side-nav__delete-memos,
.side-nav__file-bug-report {
  font-family: Roboto;
  font-size: 14px;
  outline: 0;
  height: 48px;
  padding-left: 72px;
  width: 100%;
  text-align: left;
  display: block;
  border: none;
  color: rgba(0, 0, 0, 0.87);
  cursor: pointer;
}

.side-nav__blog-post {
  background: url(./assets/ic_info_outline_24px.svg) 16px 12px no-repeat;
  line-height: 48px;
  text-decoration: none;
}

.side-nav__blog-post:focus {
  background-color: #eee;
  outline: 0;
}

.side-nav__blog-post.router-link-active {
  font-weight: 700;
  background-color: rgba(0, 0, 0, 0.05);
}

.main {
  padding-top: 72px;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
  overflow-x: hidden;
  overflow-y: auto;
  -webkit-overflow-scrolling: touch;
}

.header,
.toast-view {
  will-change: transform;
  position: fixed;
}

.header {
  width: 100%;
  height: 56px;
  color: #fff;
  background: #3f51b5;
  font-size: 20px;
  box-shadow: 0 4px 5px 0 rgba(0, 0, 0, 0.14), 0 2px 9px 1px rgba(0, 0, 0, 0.12),
    0 4px 2px -2px rgba(0, 0, 0, 0.2);
  padding: 16px 16px 0;
  display: -webkit-flex;
  display: -ms-flexbox;
  display: flex;
  -webkit-flex-direction: row;
  -ms-flex-direction: row;
  flex-direction: row;
  -webkit-flex-wrap: nowrap;
  -ms-flex-wrap: nowrap;
  flex-wrap: nowrap;
  -webkit-justify-content: flex-start;
  -ms-flex-pack: start;
  justify-content: flex-start;
  -webkit-align-items: stretch;
  -ms-flex-align: stretch;
  align-items: stretch;
  -ms-flex-line-pack: center;
  -webkit-align-content: center;
  align-content: center;
  transition: -webkit-transform 233ms cubic-bezier(0, 0, 0.21, 1) 0.1s;
  transition: transform 233ms cubic-bezier(0, 0, 0.21, 1) 0.1s;
  transition: transform 233ms cubic-bezier(0, 0, 0.21, 1) 0.1s,
    -webkit-transform 233ms cubic-bezier(0, 0, 0.21, 1) 0.1s;
  z-index: 2;
}

.header__menu {
  background: url(./assets/ic_menu_24px.svg) center center no-repeat;
  width: 24px;
  height: 24px;
  margin-right: 16px;
  text-indent: -30000px;
  overflow: hidden;
  opacity: 0.54;
  transition: opacity 333ms cubic-bezier(0, 0, 0.21, 1);
  border: none;
  outline: 0;
}

.header__menu:focus,
.header__menu:hover {
  opacity: 1;
  border: 1px solid #fff;
}

.header__title {
  font-weight: 400;
  font-size: 20px;
  margin: 0;
  -webkit-flex: 1;
  -ms-flex: 1;
  flex: 1;
}

.loader {
  left: 50%;
  top: 50%;
  position: fixed;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}

.loader #spinner {
  stroke: #673ab7;
  stroke-width: 3px;
  -webkit-transform-origin: 50%;
  transform-origin: 50%;
  -webkit-animation: line 1.6s cubic-bezier(0.4, 0, 0.2, 1) infinite,
    rotate 1.6s linear infinite;
  animation: line 1.6s cubic-bezier(0.4, 0, 0.2, 1) infinite,
    rotate 1.6s linear infinite;
}

@-webkit-keyframes rotate {
  from {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  to {
    -webkit-transform: rotate(450deg);
    transform: rotate(450deg);
  }
}

@keyframes rotate {
  from {
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  to {
    -webkit-transform: rotate(450deg);
    transform: rotate(450deg);
  }
}

@-webkit-keyframes line {
  0% {
    stroke-dasharray: 2, 85.964;
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  50% {
    stroke-dasharray: 65.973, 21.9911;
    stroke-dashoffset: 0;
  }
  100% {
    stroke-dasharray: 2, 85.964;
    stroke-dashoffset: -65.973;
    -webkit-transform: rotate(90deg);
    transform: rotate(90deg);
  }
}

@keyframes line {
  0% {
    stroke-dasharray: 2, 85.964;
    -webkit-transform: rotate(0);
    transform: rotate(0);
  }
  50% {
    stroke-dasharray: 65.973, 21.9911;
    stroke-dashoffset: 0;
  }
  100% {
    stroke-dasharray: 2, 85.964;
    stroke-dashoffset: -65.973;
    -webkit-transform: rotate(90deg);
    transform: rotate(90deg);
  }
}

.main {
  z-index: 0;
}

body:after {
  z-index: 100;
}

.side-nav {
  z-index: 200;
}

.toast-view {
  z-index: 300;
  background-color: #404040;
  border-radius: 3px;
  box-shadow: 0 0 2px rgba(0, 0, 0, 0.12), 0 2px 4px rgba(0, 0, 0, 0.24);
  color: #fff;
  line-height: 20px;
  margin-top: 8px;
  padding: 16px;
  transition: opacity 0.2s,
    -webkit-transform 0.3s cubic-bezier(0.165, 0.84, 0.44, 1);
  transition: opacity 0.2s, transform 0.3s cubic-bezier(0.165, 0.84, 0.44, 1);
  transition: opacity 0.2s, transform 0.3s cubic-bezier(0.165, 0.84, 0.44, 1),
    -webkit-transform 0.3s cubic-bezier(0.165, 0.84, 0.44, 1);
  white-space: nowrap;
  opacity: 0;
  -webkit-transform: translateY(20px);
  transform: translateY(20px);
  left: 16px;
  bottom: 16px;
}

.loader {
  z-index: 400;
}

.toast-view--visible {
  opacity: 1;
  -webkit-transform: translateY(0);
  transform: translateY(0);
}
</style>
