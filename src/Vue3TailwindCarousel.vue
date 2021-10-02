<script>
import { h } from "vue";
import Navigation from "./Navigation.vue";
export default {
  components: { Navigation },
  props: ["autoplay"],
  setup(props, { slots }) {
    const slides = slots.default().filter((slot) => slot.type.name == "slide");
    const pages = slides ? slides.length : 0;
    return { slides, pages };
  },
  data() {
    return {
      currentIndex: 0,
      initX: 0,
      finalX: 0,
      timer: null,
    };
  },
  mounted() {
    if (this.autoplay) {
      this.start();
    }
  },
  methods: {
    next() {
      this.currentIndex =
        this.currentIndex < this.pages - 1 ? this.currentIndex + 1 : 0;
      this.start();
    },
    prev() {
      this.currentIndex =
        this.currentIndex > 0 ? this.currentIndex - 1 : this.pages - 1;
      this.start();
    },
    goto(i) {
      this.currentIndex = i;
      this.start();
    },
    stop() {
      if (this.timer) {
        clearInterval(this.timer);
      }
    },
    start() {
      if (this.timer) {
        clearInterval(this.timer);
      }
      this.timer = setInterval(this.next, 4000);
    },
    dragStart(e) {
      this.initX = e.clientX;
    },
    drag(e) {
      if (!this.initX && !e.changedTouches) {
        return false;
      }
      this.stop();
      const clientX = e.clientX ?? e.changedTouches[0].clientX;
      this.initX = this.initX == 0 ? clientX : this.initX;
      this.finalX = this.initX == 0 ? 0 : clientX - this.initX;
    },
    release() {
      if (this.finalX > 30) {
        this.prev();
      } else if (this.finalX < -30) {
        this.next();
      }
      this.finalX = this.initX = 0;
      this.start();
    },
  },

  render() {
    if (this.slides) {
      this.slides.forEach((el, index) => {
        el.props = {
          ...el.props,
          index: index,
          currentIndex: this.currentIndex,
          left: this.finalX,
        };
      });
    }
    return h(
      "div",
      {
        class: "relative overflow-hidden",
        onmousedown: this.dragStart,
        ontouchmove: this.drag,
        onmousemove: this.drag,
        ontouchend: this.release,
        onmouseup: this.release,
      },
      [
        this.slides,
        h(Navigation, {
          onNext: this.next,
          onPrev: this.prev,
          onGoto: this.goto,
          pages: this.pages,
          page: this.currentIndex,
        }),
      ]
    );
  },
};
</script>