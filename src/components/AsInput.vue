<template>
  <div class="as-input">
    <input
            :value="TheInputValue"
            class="as-input__input"
            type="text"
            @input="onInputEvent($event)"
            @change="onChangeInputEvent($event)"
            @cut="onCutInputEvent"
            @copy="onCopyInputEvent"
            @paste="onPasteInputEvent"

    />
    <svg
      xmlns="http://www.w3.org/2000/svg"
      xmlns:xlink="http://www.w3.org/1999/xlink"
      viewBox="0 0 14 14"
      width="14px"
      height="14px"
      fill="#686868"
      class="as-input__close-icon"
      @click="clearInput"
      v-if="clearable || TheInputValue !== ''"
    >
      <defs>
        <path
          d="M5.293 5.293a1 1 0 011.414 0L12 10.585l5.293-5.292a1 1 0 011.32-.083l.094.083a1 1 0 010 1.414L13.415 12l5.292 5.293a1 1 0 01.083 1.32l-.083.094a1 1 0 01-1.414 0L12 13.415l-5.293 5.292a1 1 0 01-1.32.083l-.094-.083a1 1 0 010-1.414L10.585 12 5.293 6.707a1 1 0 01-.083-1.32z"
          id="a"
        />
      </defs>
      <use fill-rule="nonzero" xlink:href="#a" transform="translate(-5 -5)" />
    </svg>
  </div>
</template>

<script>
  const TYPES = [
    // button|checkbox|file|hidden|image|password|radio|reset|submit|text
    'button', 'checkbox', 'file', 'hidden', 'image', 'password', 'radio', 'reset', 'submit', 'text'

  ];
  const   formtargetkeys = [
          '_blank', '_self', '_parent', '_top'
  ];
  const formenctypekeys = [
    'application/x-www-form-urlencoded',
    'multipart/form-data',
    'text/plain'
  ];
  const alignkeys = [
    'bottom', 'left', 'middle', 'right', 'top'
  ];

export default {
  props: {
    dataInput: {
      type: String,
    },
    clearable: {
      type: Boolean,
      default: false,
    },
    autocomplete: {
      type: String,
      default: 'off'
    },
    accesskey: {
      type: [Number, String]
    },
    alt: {
      type: String,
    },
    align: {
    //  "bottom | left | middle | right | top"
      type: String,
      default: 'bottom',
      validator: type => alignkeys.includes(type)
    },
    autofocus: {
      type: Boolean,
      default: false
    },
    border: {
      type: Number,
      default: 0
    },
    checked: {
      type: Boolean,
      default: false
    },
    disabled: {
      type: Boolean,
      default: false
    },
    form: {
      type: String
    },
    formaction: {
      type: String
    },
    formenctype: {
      // application/x-www-form-urlencoded
      // multipart/form-data
      // text/plain
      type: String,
      default: 'application/x-www-form-urlencoded',
      validator: type => formenctypekeys.includes(type)
    },
    formmethod: {
      // get post
      type: String
    },
    formnovalidate: {
      type: Boolean,
      default: false
    },
    formtarget: {
      //  <имя окна> | _blank | _self | _parent | _top
      type: String,
      validator: type => formtargetkeys.includes(type)
    },
    list: {
      // Значение Имя идентификатора тега <datalist>.
      type: String
    },
    max: {
      type: [Number, Date],
    },
    maxlength: {
      type: Number
    },
    min: {
      type: [Number, Date],
    },
    multiple: {
      type: Boolean,
      default: false
    },
    name: {
      type: String
    },
    pattern: {
      type: RegExp
    },
    placeholder: {
      type: String
    },
    readonly: {
      type: Boolean,
      default: false
    },
    required: {
      type: Boolean,
      default: false
    },
    size: {
      type: Number
    },
    src: {
      type: String
    },
    step: {
      type: Number
    },
    tabindex: {
      type: Number
    },
    type: {
      // button|checkbox|file|hidden|image|password|radio|reset|submit|text
      required: true,
      type: String,
      default: 'text',
      validator: type => TYPES.includes(type),
    },
    value: {
      type: String,
      default: ''
    }



  },
  data() {
    return {
      TheInputValue: this.value,
    };
  },

  methods: {
    clearInput() {
      this.TheInputValue = "";
      this.$emit("input", "");
    },
    onInputEvent($event){
      this.TheInputValue = $event.target.value;
      this.$emit('input', $event.target.value);
    },
    onChangeInputEvent($event){
      this.$emit('chenge', $event);
    },
    onCutInputEvent($event){
      this.$emit('cut', $event);
    },
    onCopyInputEvent($event){
      this.$emit('copy', $event);
    },
    onPasteInputEvent($event){
      this.$emit('paste', $event);
    }

  },

};
</script>

<style lang="scss">
.as-input {
  display: flex;
  width: 200px;
  position: relative;
  &__input {
    padding: 10px;
    color: #686868;
    border-radius: 5px;
    width: 100%;
  }
  &__close-icon {
    border: 1px solid #686868;
    position: absolute;
    border-radius: 50%;
    padding: 5px;
    margin-top: 5px;
    right: 20px;
    :hover {
      cursor: pointer;
    }
  }
}
</style>
