<template lang="html">
    <div :class="['ui', getSlotsClasses(), getIconClasses(), getSizeClasses(),
        { 'fluid' : fluid }, { 'inverted' : inverted },
        { 'transparent' : transparent }, { 'disabled' : disabled }, 'input',
        { 'loading' : loading }, { 'error' : error }]">
        <slot name="left-label"></slot>
        <slot name="left-action"></slot>
        <input
            :id="id"
            :accept="accept"
            :alt="alt"
            :autocomplete="autocomplete"
            :autofocus="autofocus"
            :checked="checked"
            :dirname="dirname"
            :disabled="disabled"
            :form="form"
            :formaction="formaction"
            :formenctype="formenctype"
            :formmethod="formmethod"
            :formnovalidate="formnovalidate"
            :formtarget="formtarget"
            :list="list"
            :max="max"
            :maxlength="maxlength"
            :min="min"
            :multiple="multiple"
            :name="name"
            :pattern="pattern"
            :placeholder="placeholder"
            :readonly="readonly"
            :required="required"
            :src="src"
            :step="step"
            :type="type"
            :value="value"
            @keydown="emitKeyDown"
            @keypress="emitKeyPress"
            @keyup="emitKeyUp"
            @mouseenter="emitMouseEnter"
            @mouseover="emitMouseOver"
            @mousemove="emitMouseMove"
            @mousedown="emitMouseDown"
            @mouseup="emitMouseUp"
            @click="emitClick"
            @dblclick="emitDoubleClick"
            @wheel="emitWheel"
            @mouseleave="emitMouseLeave"
            @mouseout="emitMouseOut"
            @pointerlockchange="emitPointerLockChange"
            @pointerlockerror="emitPointerLockError"
            @blur="emitBlur"
            @change="emitChange($event.target.value)"
            @contextmenu="emitContextMenu"
            @focus="emitFocus"
            @input="emitInput($event.target.value)"
            @invalid="emitInvalid"
            @reset="emitReset"
            @search="emitSearch"
            @select="emitSelect"
            @submit="emitSubmit"
            ref="input" />
        <slot name="right-label"></slot>
        <slot name="right-action"></slot>
        <i :class="[dIcon.value, 'icon']" v-if="dIcon.value"></i>
    </div>
</template>

<script>
import Constants from '../mixins/commons/constants.js'
import Input from '../mixins/commons/input/index'
import RandomProp from '../mixins/commons/props/random.js'
import Loading from '../mixins/commons/states/loading.js'
import Error from '../mixins/commons/states/error.js'
import Icon from '../mixins/commons/icon.js'
import Inverted from '../mixins/commons/inverted.js'
import Size from '../mixins/commons/sizes/six.js'

export default {
    mixins: [Input, Loading, Error, Icon, Inverted, Size],
    data() {
        return {
            dIcon: {
                value: this.icon,
                position: this.iconPosition
            },
        }
    },
    props: {
        id: RandomProp,
        transparent: {
            type: Boolean,
            required: false,
            default: false,
            // validator(value) {
            //     return true
            // },
        },
        fluid: {
            type: Boolean,
            required: false,
            default: false,
            // validator(value) {
            //     return true
            // },
        }
    },
    created() {
        if (this.loading && !this.icon) {
            this.dIcon.value = 'notched circle loading';
            this.dIcon.position = Constants.left;
        }

        if (this.leftIcon) {
            this.dIcon.value = this.leftIcon;
            this.dIcon.position = Constants.left;
        }
    },
    methods: {
        getIconClasses() {
            if (this.dIcon.value) {
                return (this.dIcon.position == Constants.right ? Constants.icon : this.dIcon.position + ' ' + Constants.icon)
            }

            return false
        },
        getSlotsClasses() {
            var classes = []

            if (this.$slots.hasOwnProperty('right-label')) {
                classes.push(Constants.right)
            }

            if (
                    this.$slots.hasOwnProperty('left-label') || this.$slots.hasOwnProperty('right-label')
                ) {
                classes.push(Constants.labeled)
            }

            if (this.$slots.hasOwnProperty('left-action')) {
                classes.push(Constants.left)
            }

            if (this.$slots.hasOwnProperty('left-action') || this.$slots.hasOwnProperty('right-action')) {
                classes.push(Constants.action)
            }

            return classes;
        },
        blur() {
            this.$refs.input.blur()
        },
        focus() {
            this.$refs.input.focus()
        },
    }
}
</script>

<docs lang="md">
    # Input

    ```html
    <ui-input placeholder="Search…" left-icon="search" />
    <ui-input placeholder="Search…">
    	<button class="ui button" slot="right-action">Search</button>
    </ui-input>
    <ui-input placeholder="Search…" size="large">
        <ui-label slot="left-label">Search</ui-label>
        <i class="search icon" slot="left-icon"></i>
        <ui-label slot="right-label">Search</ui-label>
    </ui-input>
    ```

    # Output

    ```html
    <div class="ui left icon input">
        <input type="text" placeholder="Search…">
        <i class="search icon"></i>
    </div>
    <div class="ui action input">
    	<input type="text" placeholder="Search…">
        <button class="ui button">Search</button>
    </div>
    <div class="ui right labeled large input">
    	<div class="ui label">Search</div>
        <input type="text" placeholder="Search…">
        <div class="ui label">Search</div>
    </div>
    ```
</docs>
