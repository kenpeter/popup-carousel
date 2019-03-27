<script>
  export default {
    name: 'modal',

    // list of methods
    methods: {
      // close
      close() {
        // this is @close
        this.$emit('close');
      },

      next () {
        const first = this.slides.shift()
        this.slides = this.slides.concat(first)
      },

      previous () {
        const last = this.slides.pop()
        this.slides = [last].concat(this.slides)
      }
    },

    data () {
      return {
        slides: [
          {
            title: 'I am Slide A',
            id: 1
          },
          {
            title: 'I am Slide B',
            id: 2
          },
          {
            title: 'I am Slide C',
            id: 3
          },
          {
            title: 'I am Slide D',
            id: 4
          },
          {
            title: 'I am Slide E',
            id: 5
          }
        ]
      }
    },
  };
</script>

<template>
    <div class="modal-backdrop">
        <div class="modal">
            <header class="modal-header">
                <slot name="header">
                    This is the default tile!

                    <button
                            type="button"
                            class="btn-close"
                            @click="close"
                    >
                        x
                    </button>
                </slot>
            </header>
            <section class="modal-body">
                <slot name="body">
                    <div class='carousel-view'>
                        <transition-group
                                class='carousel'
                                tag="div">
                            <div
                                    v-for="slide in slides"
                                    class='slide'
                                    :key="slide.id">
                                <h4> {{ slide.title }} </h4>
                            </div>
                        </transition-group>
                        <div class='carousel-controls'>
                            <button class='carousel-controls__button' @click="previous">prev</button>
                            <button class='carousel-controls__button' @click="next">next</button>
                        </div>
                    </div>
                </slot>
            </section>
            <footer class="modal-footer">
                <slot name="footer">
                    I'm the default footer!


                </slot>
            </footer>
        </div>
    </div>
</template>

<style>
    .modal-backdrop {
        position: fixed;
        top: 0;
        bottom: 0;
        left: 0;
        right: 0;
        background-color: rgba(0, 0, 0, 0.3);
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        background: #FFFFFF;
        box-shadow: 2px 2px 20px 1px;
        overflow-x: auto;
        display: flex;
        flex-direction: column;
    }

    .modal-header,
    .modal-footer {
        padding: 15px;
        display: flex;
    }

    .modal-header {
        border-bottom: 1px solid #eeeeee;
        color: #4AAE9B;
        justify-content: space-between;
    }

    .modal-footer {
        border-top: 1px solid #eeeeee;
        justify-content: flex-end;
    }

    .modal-body {
        position: relative;
        padding: 20px 10px;
    }

    .btn-close {
        border: none;
        font-size: 20px;
        padding: 20px;
        cursor: pointer;
        font-weight: bold;
        color: #4AAE9B;
        background: transparent;
    }

    .btn-green {
        color: white;
        background: #4AAE9B;
        border: 1px solid #4AAE9B;
        border-radius: 2px;
    }


    
    .carousel-view {
        display: flex;
        flex-direction: column;
        align-items: center;
    }

    .carousel {
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;

        width: 24em;
        min-height: 25em;
    }

    .slide {
        flex: 0 0 20em;
        height: 10em;
        margin: 1em;

        display: flex;
        justify-content: center;
        align-items: center;

        /*
        border: 0.1em dashed #000;
        border-radius: 50%;*/

        border: 0.1em solid #000;

        transition: transform 0.3s ease-in-out;
    }

    .slide:first-of-type {
        opacity: 0;
    }

    .slide:last-of-type {
        opacity: 0;
    }
</style>
