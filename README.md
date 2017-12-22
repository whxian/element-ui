# element-ui_input-maxlength

配置element-ui【源码】中输入内容提供对应输入建议时的最大长度问题


---

1.  要想给input框点击可以列出输入建议
```javascript
<el-col :span="12">
  <div class="sub-title">激活即列出输入建议</div>
  <el-autocomplete
    class="inline-input"
    v-model="state1"
    :fetch-suggestions="querySearch"
    placeholder="请输入内容"
    @select="handleSelect"
  ></el-autocomplete>
</el-col>
```

  2.  并且当输入的时候限制最大长度

>在源码里给autocomplete增加maxlength可以限制输入的最大长度，但此时除了autocomplete其余所有的input的maxlength属性全部失效，变为maxlength="off"，所以需要在ElInput的所有props里增加`maxlength: Number`字段，此时所有的input框（包括autocomplete）全部生效。
```javascript
/* 65 */
    /***/ function (module, exports) {

        module.exports = {
            render: function () {
                var _vm = this;
                var _h = _vm.$createElement;
                var _c = _vm._self._c || _h;
                return _c('div', {
                    class: [
                        _vm.type === 'textarea' ? 'el-textarea' : 'el-input',
                        _vm.size ? 'el-input--' + _vm.size : '', {
                            'is-disabled': _vm.disabled,
                            'el-input-group': _vm.$slots.prepend || _vm.$slots.append,
                            'el-input-group--append': _vm.$slots.append,
                            'el-input-group--prepend': _vm.$slots.prepend
                        }
                    ]
                }, [(_vm.type !== 'textarea') ? [(_vm.$slots.prepend) ? _c('div', {
                            staticClass: "el-input-group__prepend"
                        }, [_vm._t("prepend")], 2) : _vm._e(), _vm._t("icon", [(_vm.icon) ? _c('i', {
                            staticClass: "el-input__icon",
                            class: [
                                'el-icon-' + _vm.icon,
                                _vm.onIconClick ? 'is-clickable' : ''
                            ],
                            on: {
                                "click": _vm.handleIconClick
                            }
                        }) : _vm._e()]), (_vm.type !== 'textarea') ? _c('input', _vm._b({
                            ref: "input",
                            staticClass: "el-input__inner",
                            attrs: {
                                "autocomplete": _vm.autoComplete,
                                "maxlength": _vm.maxlength,
                            },
                            domProps: {
                                "value": _vm.currentValue
                            },
                            on: {
                                "input": _vm.handleInput,
                                "focus": _vm.handleFocus,
                                "blur": _vm.handleBlur
                            }
                        }, 'input', _vm.$props)) : _vm._e(), (_vm.validating) ? _c('i', {
                            staticClass: "el-input__icon el-icon-loading"
                        }) : _vm._e(), (_vm.$slots.append) ? _c('div', {
                            staticClass: "el-input-group__append"
                        }, [_vm._t("append")], 2) : _vm._e()] : _c('textarea', _vm._b({
                        ref: "textarea",
                        staticClass: "el-textarea__inner",
                        style: (_vm.textareaStyle),
                        domProps: {
                            "value": _vm.currentValue
                        },
                        on: {
                            "input": _vm.handleInput,
                            "focus": _vm.handleFocus,
                            "blur": _vm.handleBlur
                        }
                    }, 'textarea', _vm.$props))], 2)
            }, staticRenderFns: []
        }

        /***/
    },
```
