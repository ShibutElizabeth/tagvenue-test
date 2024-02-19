<template>
    <div :class="$style.box">
        <label :class="$style.box__label">{{ label }}</label>
        <input 
            :class="[$style.box__input,  checkInvalidUrl(urlValue) ? $style.box__input_error : '']" 
            type=text 
            v-model="urlValue" 
            @input="emitUrlValue" 
            :placeholder="placeholder" />
    </div>
</template>

<script>
export default {
    name: "URLInput",
    props: {
        label: {
            type: String,
            default: ''
        },
        placeholder: {
            type: String,
            default: 'https://hello.com'
        },
        checkInvalidUrl: {
            type: Function,
            default: () => {}
        }
    },
    data() {
      return {
        urlValue: '',
      };
    },
    methods: {
        emitUrlValue() {
            this.$emit('check-input', this.urlValue);
        }
    }
};
</script>
  
<style module>
.box{
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.box__label{
    font-size: 1.125rem;
    font-weight: 400;
}

.box__input{
    position: relative;
    background-color: transparent;
    border: none;
    border-bottom: 1px solid var(--brand-light);
    color: var(--brand-light);
    font-size: 1rem;
    text-align: left;
    resize: none;   
}
.box__input::placeholder{
    color: var(--brand-light);
    opacity: 0.5;
}
.box__input:focus{
    border: none;
    outline: none;
    border-bottom: 1px solid var(--brand-light);
}

.box__input_error{
    border-bottom: 1px solid var(--brand-danger);
}
</style>
  