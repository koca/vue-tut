<template>
  <intersect root-margin="-260px 0px 0px 0px" @enter="intersected = true" @leave="intersected = false">
    <div :class="intersectedClass" class="step-wrapper">
      <div class="step-container">
        <div class="step p-w-med p-e-xl p-n-lg p-s-lg">
          <main>
            <label class="step-label m-s-med">
              <!-- The name of the step -->
              <slot name="name">
                <!-- "Step #"-->
                <template v-if="!$slots.name && index">
                  Step {{ index }}
                </template>
              </slot>
            </label>

            <!-- The content of the step box -->
            <slot />
          </main>
        </div>

        <div class="step-aside">
          <!-- The content to put aside the step box (or below on mobile) -->
          <slot name="aside" />
        </div>
      </div>

      <div class="step-after">
        <!-- Content to display after and outside the step box -->
        <slot name="after" />
      </div>
    </div>
  </intersect>
</template>

<script>
import Intersect from 'vue-intersect';

export default {
  name: 'TutorialStep',

  components: {
    Intersect
  },

  data () {
    return {
      intersected: false,
      index: null
    };
  },

  computed: {
    intersectedClass() {
      return this.intersected ? 'step-intersected' : '';
    }
  },

  mounted() {
    let index = Array.prototype.indexOf.call(this.$el.parentNode.children, this.$el);
    this.index = index + 1;
  }
};
</script>
