<template lang="html">
    <div :class="['ui', getSizeClasses(), 'label']">
        <slot></slot>
    </div>
</template>

<script>
import Size from '../mixins/commons/sizes/eight.js'

export default {
    mixins: [Size]
}
</script>
