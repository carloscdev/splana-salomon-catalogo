<template>
  <div class="book">
    <vue-book-effects
      class="book-effects"
      :pages="pages"
      :pagesHiRes="pagesHiRes"
      :startPage="pageNum"
      v-slot="bookEffects"
      ref="bookEffects"
      @flip-left-start="onFlipLeftStart"
      @flip-left-end="onFlipLeftEnd"
      @flip-right-start="onFlipRightStart"
      @flip-right-end="onFlipRightEnd"
      @zoom-start="onZoomStart"
      @zoom-end="onZoomEnd"
    >
      <div class="action-bar">
        <i class="fas fa-arrow-left btn left" :class="{ disabled: !bookEffects.canFlipLeft }" @click="bookEffects.flipLeft"></i>
        <i class="fas fa-plus btn plus" :class="{ disabled: !bookEffects.canZoomIn }" @click="bookEffects.zoomIn"></i>
        <span class="page-num"> Página {{ bookEffects.page }} de {{ bookEffects.numPages }} </span>
        <i class="fas fa-minus btn minus" :class="{ disabled: !bookEffects.canZoomOut }" @click="bookEffects.zoomOut"></i>
        <i class="fas fa-arrow-right btn right" :class="{ disabled: !bookEffects.canFlipRight }" @click="bookEffects.flipRight"></i>
      </div>
    </vue-book-effects>
  </div>
</template>

<script>
import VueBookEffects from 'vue-book-effects'
export default {
  name: 'Catalogo',
  components: { VueBookEffects },
  data() {
    return {
      pages: [],
      pagesHiRes: [],
      hasMouse: true,
      pageNum: 1
    }
  },
  mounted() {
    window.addEventListener('keydown', ev => {
      const bookEffects = this.$refs.bookEffects
      if (!bookEffects) {
        return
      }
      if (ev.keyCode === 37 && bookEffects.canFlipLeft) {
        bookEffects.flipLeft()
      }
      if (ev.keyCode === 39 && bookEffects.canFlipRight) {
        return bookEffects.flipRight()
      }
    })
    setTimeout(() => {
      this.pages = [
        null,
        'https://images.unsplash.com/photo-1624367171718-14026220ee35?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80',
        'https://i.postimg.cc/YC2crk35/FADED-VIOLINES-1.jpg',
        'https://i.postimg.cc/9FY5HzGP/FADED-VIOLINES-2.jpg',
        'https://i.postimg.cc/v87Sckcb/VIOLIN-MI-CORAZON-ENCANTADO-1.jpg',
        'https://i.postimg.cc/gjKMQXfn/VIOLIN-MI-CORAZON-ENCANTADO-2.jpg',
        'https://i.postimg.cc/7LgSK8vL/violines-himno-a-la-alegria-1.jpg',
        'https://i.postimg.cc/R0XBb8NV/TITANIC.jpg'
      ]
      this.pagesHiRes = [
        null,
        'https://images.unsplash.com/photo-1624367171718-14026220ee35?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=687&q=80',
        'https://i.postimg.cc/YC2crk35/FADED-VIOLINES-1.jpg',
        'https://i.postimg.cc/9FY5HzGP/FADED-VIOLINES-2.jpg',
        'https://i.postimg.cc/v87Sckcb/VIOLIN-MI-CORAZON-ENCANTADO-1.jpg',
        'https://i.postimg.cc/gjKMQXfn/VIOLIN-MI-CORAZON-ENCANTADO-2.jpg',
        'https://i.postimg.cc/7LgSK8vL/violines-himno-a-la-alegria-1.jpg',
        'https://i.postimg.cc/R0XBb8NV/TITANIC.jpg'
      ]
    }, 1)
    window.addEventListener('hashchange', this.setPageFromHash)
    this.setPageFromHash()
  },
  methods: {
    onFlipLeftStart(page) {
      return console.log('flip-left-start', page)
    },
    onFlipLeftEnd(page) {
      console.log('flip-left-end', page)
      return (window.location.hash = '#' + page)
    },
    onFlipRightStart(page) {
      return console.log('flip-right-start', page)
    },
    onFlipRightEnd(page) {
      console.log('flip-right-end', page)
      return (window.location.hash = '#' + page)
    },
    onZoomStart(zoom) {
      return console.log('zoom-start', zoom)
    },
    onZoomEnd(zoom) {
      return console.log('zoom-end', zoom)
    },
    setPageFromHash() {
      const n = parseInt(window.location.hash.slice(1), 10)
      if (isFinite(n)) {
        return (this.pageNum = n)
      }
    }
  }
}
</script>
<style>
.action-bar {
  width: 100%;
  height: 40px;
  padding-top: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.action-bar .btn {
  color: rgb(192, 192, 192);
  border: 1px solid rgb(192, 192, 192);
  border-radius: 50%;
  padding-top: 7px;
  cursor: pointer;
  font-size: 14px;
  width: 30px;
  height: 30px;
  text-align: center;
}
.action-bar .btn:not(:first-child) {
  margin-left: 10px;
}
.action-bar .btn:hover {
  color: rgb(192, 192, 192);
  filter: drop-shadow(1px 1px 5px #000);
}
.action-bar .btn:active {
  filter: none !important;
}
.action-bar .btn.disabled {
  pointer-events: none;
  opacity: 0.2;
}
.action-bar .page-num {
  font-size: 12px;
  margin-left: 10px;
}
.book-effects .viewport {
  width: 90vw;
  height: calc(100vh - 50px - 40px);
}
.book-effects .bounding-box {
  box-shadow: 0 0 20px #000;
}
</style>
