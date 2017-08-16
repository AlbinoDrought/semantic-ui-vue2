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
