<template lang="html">
    <div :class="[getWidthClasses(), { 'inline' : inline },
        { 'required' : required }, { 'disabled' : disabled }, 'field',
        { 'error' : error }]">
        <label :for="id">
            {{ label }}
            <slot name="label"></slot>
        </label>
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
            v-on:keydown="emitKeyDown"
            v-on:keypress="emitKeyPress"
            v-on:keyup="emitKeyUp"
            v-on:mouseenter="emitMouseEnter"
            v-on:mouseover="emitMouseOver"
            v-on:mousemove="emitMouseMove"
            v-on:mousedown="emitMouseDown"
            v-on:mouseup="emitMouseUp"
            v-on:click="emitClick"
            v-on:dblclick="emitDoubleClick"
            v-on:wheel="emitWheel"
            v-on:mouseleave="emitMouseLeave"
            v-on:mouseout="emitMouseOut"
            v-on:pointerlockchange="emitPointerLockChange"
            v-on:pointerlockerror="emitPointerLockError"
            v-on:blur="emitBlur"
            v-on:change="emitChange($event.target.value)"
            v-on:contextmenu="emitContextMenu"
            v-on:focus="emitFocus"
            v-on:input="emitInput($event.target.value)"
            v-on:invalid="emitInvalid"
            v-on:reset="emitReset"
            v-on:search="emitSearch"
            v-on:select="emitSelect"
            v-on:submit="emitSubmit"
            ref="input" />
    </div>
</template>

<script>
import Input from '../../mixins/commons/input/index'
import RandomProp from '../../mixins/commons/props/random.js'
import Error from '../../mixins/commons/states/error.js'
import Width from '../../mixins/commons/width.js'

export default {
    mixins: [Input, Error, Width],
    props: {
        label: {
            type: String,
        },
        id: RandomProp,
        inline: {
            type: Boolean,
            required: false,
            default: false,
        },
    }
}
</script>
