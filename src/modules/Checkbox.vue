<template lang="html">
    <div :class="['ui', { 'disabled' : disabled }, { 'fitted' : fitted },
        { 'read-only' : readonly }, { 'checked' : isChecked() },
        { 'disabled' : disabled }, typeClass, 'checkbox', { 'focus' : focus },
        { 'error' : error }]">
        <input
            :id="id"
            :accept="accept"
            :alt="alt"
            :autocomplete="autocomplete"
            :autofocus="autofocus"
            :checked="isChecked()"
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
            :type="inputType"
            :value="inputValue"
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
            <label :for="id">
                <slot>{{ label }}</slot>
            </label>
    </div>
</template>

<script>
    import Constants from '../mixins/commons/constants.js'
    import Input from '../mixins/commons/input/index'
    import RandomProp from '../mixins/commons/props/random.js'
    import Focus from '../mixins/commons/states/focus.js'
    import Error from '../mixins/commons/states/error.js'

    const types = [
        Constants.checkbox,
        Constants.radio,
        Constants.slider,
        Constants.toggle,
    ]

    const inputTypes = [
        Constants.checkbox,
        Constants.radio,
    ]

    export default {
        mixins: [Input, Focus, Error],
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
            checked: {
                type: Boolean,
                default: undefined,
            },
            fitted: {
                type: Boolean,
                default: false,
            },
            inputType: {
                type: String,
                required: false,
                default() {
                    return this.type == Constants.radio ? Constants.radio : Constants.checkbox
                },
                validator(value) {
                    return inputTypes.indexOf(value) > -1
                }
            },
            label: {
                type: String,
                required: false,
            },
            type: {
                type: String,
                required: false,
                default: Constants.checkbox,
                validator(value) {
                    return types.indexOf(value) > -1;
                },
            },
        },
        computed: {
            typeClass() {
                return thiindexs.type != Constants.checkbox ? this.type : false
            },
            inputValue() {
                var attrs = this.$vnode.data.attrs

                if (typeof attrs != 'undefined' && attrs.value) {
                    return attrs.value
                }

                if (this.inputType != Constants.radio && this.trueVal) {
                    return this.trueVal
                }

                return this.value
            },
            trueVal() {
                if (typeof this.$vnode.data.attrs == 'undefined') {
                    return null;
                }

                return this.$vnode.data.attrs['true-value'];
            },
            falseVal() {
                if (typeof this.$vnode.data.attrs == 'undefined') {
                    return null;
                }

                return this.$vnode.data.attrs['false-value'];
            },
        },
        methods: {
            emitChange(value) {
                var input = this.$refs.input;

                if (this.inputType == Constants.radio && this.isChecked()) {
                    this.$emit('input', this.inputValue);
                }

                if (Array.isArray(this.value)) {
                    var result = this.value;
                    var index = this.value.indexOf(this.inputValue);

                    if (index == -1 && input.checked) {
                        result.push(this.inputValue);
                    }

                    if (index > -1 && !input.checked) {
                        result.splice(index, 1);
                    }

                    // https://forum.vuejs.org/t/custom-checkbox-component/1120/8
                    this.$emit('input', result);
                } else {
                    if (this.trueVal || this.falseVal) {
                        if (this.trueVal && input.checked) {
                            this.$emit('input', this.trueVal);
                        }

                        if (this.falseVal && !input.checked) {
                            this.$emit('input', this.falseVal);
                        }
                    } else {
                        if (this.inputType == Constants.radio) {
                            this.$emit('input', this.inputValue);
                        } else {
                            this.$emit('input', !this.value);
                        }
                    }
                }

                this.$emit('change', this.isChecked());
            },
            usesVueModel() {
                return typeof this.$vnode.data.attrs != 'undefined'
                    && this.$vnode.data.attrs.value
                    && Array.isArray(this.value)
            },
            isChecked() {
                if (this.usesVueModel()) {
                    return this.value.indexOf(this.inputValue) > -1
                }

                if (this.inputType == Constants.radio) {
                    return this.value == this.$vnode.data.attrs.value;
                }

                if (this.value !== true && this.value !== false) {
                    return this.value == this.trueVal
                }

                return this.value
            },
            isUnchecked() {
                return !this.isChecked()
            },
        },
    }
</script>

<style scoped>
    .ui.checkbox label {
        cursor: pointer;
        user-select: none;
    }
</style>

<docs type="md">
    `v-model` has to be an `array` if you want to track multiple selections
</docs>

