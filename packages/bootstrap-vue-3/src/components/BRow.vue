<template>
  <component :is="tag" class="row" :class="[classes, rowColsClasses]">
    <slot />
  </component>
</template>

<script lang="ts">
import {computed, defineComponent, PropType} from 'vue'
import {getBreakpointProps, getClasses} from '../utils'
import type {Alignment} from '../types'

const rowColsProps = getBreakpointProps('cols', [''], {type: [String, Number], default: null})

export default defineComponent({
  props: {
    tag: {type: String, default: 'div'},
    gutterX: {type: String, default: null},
    gutterY: {type: String, default: null},
    alignV: {type: String as PropType<Alignment.Vertical>, default: null},
    alignH: {type: String as PropType<Alignment.Horizontal>, default: null},
    alignContent: {type: String as PropType<Alignment.Content>, default: null},
    ...rowColsProps,
  },
  setup(props) {
    const rowColsClasses = getClasses(props, rowColsProps, 'cols', 'row-cols')

    const classes = computed(() => ({
      [`gx-${props.gutterX}`]: props.gutterX !== null,
      [`gy-${props.gutterY}`]: props.gutterY !== null,
      [`align-items-${props.alignV}`]: props.alignV,
      [`justify-content-${props.alignH}`]: props.alignH,
      [`align-content-${props.alignContent}`]: props.alignContent,
    }))

    return {
      classes,
      rowColsClasses,
    }
  },
})
</script>
