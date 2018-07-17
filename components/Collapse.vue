<template>
  <div class="accordion">
    <div class="accordion-header" :class="headerClass" @click="toggle">
      <slot name="header">
      </slot>
      <i class="fas fa-chevron-down" :class="{ rotate: isShown }"></i>
    </div>
    <transition name="accordion"
      v-on:before-enter="beforeEnter" v-on:enter="enter"
      v-on:before-leave="beforeLeave" v-on:leave="leave">
      <div class="accordion-body" v-if="isShown">
        <slot>
        </slot>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    },
    headerClass: {
      type: String,
      default: ''
    }
  },

  data: () => ({
    isShown: false
  }),

  mounted () {
    this.isShown = this.show
  },

  methods: {
    toggle () {
      this.isShown = !this.isShown
    },

    beforeEnter (el) {
      el.style.height = '0';
    },

    enter (el) {
      el.style.height = 'auto';
    },

    beforeLeave (el) {
      el.style.height = 'auto';
    },

    leave (el) {
      el.style.height = '0';
    }
  }
}
</script>

<style lang="scss" scoped>
.accordion {
  .accordion-header {
    position: relative;
    cursor: pointer;
  }

  .accordion-header i {  
    position: absolute;
    top: 12px;
    right: 0;
    transform: rotate(0deg);
    transition-duration: 0.3s;
    font-size: 0.75rem;
  }

  .accordion-header i.rotate {  
    transform: rotate(180deg);
    transition-duration: 0.3s;
  }
}
</style>
