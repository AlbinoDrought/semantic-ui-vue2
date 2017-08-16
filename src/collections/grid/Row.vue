<template lang="html">
    <div :class="[getFloatClasses(), getAlignClasses(),getEqualWidthClasses(), getColumnClasses(), { 'centered' : centered }, 'row']">
      <slot></slot>
    </div>
</template>

<script>
import EqualWidth from '../../mixins/commons/equal-width.js'
import Column from '../../mixins/commons/column.js'
import Align from '../../mixins/commons/align.js'
import Float from '../../mixins/commons/float.js'
import Centered from '../../mixins/commons/centered.js'

export default {
    mixins: [EqualWidth, Column, Align, Float, Centered],
}
</script>
