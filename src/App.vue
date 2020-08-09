<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <h1 class="animated bounce">Animations</h1>
        <hr />
        <button class="btn btn-primary" @click="showAlert = !showAlert">Show Alert</button>
        <br />
        <br />
        <transition name="fade">
          <div v-if="showAlert" class="alert alert-info">This is some info</div>
        </transition>
        <transition name="slide" type="animation">
          <div v-show="showAlert" class="alert alert-info">This is some info</div>
        </transition>
        <transition
          name="custom-classes-transition"
          enter-active-class="animated bounceInRight"
          leave-active-class="animated bounceOutRight"
        >
          <div v-if="showAlert" class="alert alert-info">This is some info</div>
        </transition>
        <!-- 4 -->

        <transition name="slide" mode="out-in">
          <div v-if="showAlert" class="alert alert-info" key="info">This is some info</div>
          <div v-else class="alert alert-warning" key="warning">This is some Warning</div>
        </transition>

        <hr style="color: yellow; background-color: chartreuse;">
        <button class="btn btn-primary" @click="load = !load">Load/Remove Element</button>
        <br><br>
        <transition
          @before-enter="berforeEnter"
          @enter="enter"
          @after-enter="afterEnter"
          @enter-cancelled="enterCancelled"

          @before-leave="berforeLeave"
          @leave="leave"
          @after-leave="afterLeave"
          @leave-cancelled="leaveCancelled"
          :css="false"
        >
          <div style="height:100px; width:100px; background-color: lightgreen" v-if="load"></div>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showAlert: false,
      load: false
    };
  },
  methods: {
    berforeEnter(el) {
    console.log("berforeEnter -> berforeEnter", el)
    },
    enter(el, done) {
      console.log("Enter");
      done();

    },
    afterEnter(el) {
    console.log("afterEnter -> el", el);      
    },
    enterCancelled(el) {
    console.log("enterCancelled -> el", el);
    },

    berforeLeave(el) {
    console.log("beforeLeave -> el", el)

    },
    leave(el, done) {
    console.log("leave -> el", el)
    done();
    },
    afterLeave(el) {
    console.log("afterLeave -> el", el)
      
    },
    leaveCancelled(el) {
    console.log("leaveCancelled -> el", el)

    },
    
  }
};
</script>

<style>
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  transition: opacity 1s;
}
.fade-leave {
  /* opacity: 1; */
}
.fade-leave-active {
  transition: opacity 1s;
  opacity: 0;
}
.slide-enter {
  /* transform: translateY(20px); */
  opacity: 0;
}
.slide-enter-active {
  animation: slide-in 1s ease-out forwards;
  transition: opacity 0.5s;
}
.slide-leave {
}
.slide-leave-active {
  animation: slide-out 1s ease-out forwards;
  transition: opacity 1s;
  opacity: 0;
}

@keyframes slide-in {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0);
  }
}
@keyframes slide-out {
  from {
    transform: translateY(0px);
  }
  to {
    transform: translateY(20px);
  }
}
</style>
