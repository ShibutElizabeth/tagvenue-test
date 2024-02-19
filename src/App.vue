<template>
    <div :class="$style.container">
        <div :class="$style.form">
            <URLInput label="New URL (https only)" @checkInput="updateFirstUrl"></URLInput>
            <URLInput label="Confirm URL" @checkInput="updateSecondUrl"></URLInput>
            
            <div :class="$style.errors">
                <Error message="Provided URLs must be the same!" v-show="equalityError"></Error>
                <Error message="Provided URL must be a valid https link!" v-show="invalidError"></Error>
            </div>
            <button :class="$style.button" @click="checkUrls">Save</button>
        </div>
    </div>
  </template>
  
<script>

import URLInput from "./components/URLInput.vue";
import Error from "./components/Error.vue";
import { addNewUrl } from "./api";

export default {
    name: "App",
    data() {
        return {
            firstUrl: '',
            secondUrl: '',
            invalidError: false,
            equalityError: false,
        };
    },
    components: {
        URLInput,
        Error
    },
    methods: {
        updateFirstUrl(value) {
            this.firstUrl = value.replaceAll(' ', '');
        },
        updateSecondUrl(value) {
            this.secondUrl = value.replaceAll(' ', '');
        },
        checkEquality() {
            if (this.firstUrl === this.secondUrl) {
                this.equalityError = false;
            } else {
                console.log('error!');
            }
        },
        checkUrls(){
            this.equalityError = this.isNotEqual;
            this.invalidError = this.isInvalidUrl;
            if(!this.equalityError && !this.invalidError){
                this.submit();
            } else{
                console.log('wrong!')
            }
        },
        submit() {
            console.log('submit')
            addNewUrl().then(function () {
                alert('Saved!');
            });
            
        },
    },
    computed: {
        isNotEqual() {
            return this.firstUrl !== this.secondUrl;
        },
        isInvalidUrl() {
            const urlRegex = /^https:\/\/[^\s/$.?#].[^\s]*$/;
            return !urlRegex.test(this.firstUrl) || !urlRegex.test(this.secondUrl);
        }
    },
};
</script>
  
<style module>
:root {
    --brand-danger: #ff0000;
    --brand-dark: #232325;
    --brand-light: #ffffff;
    --brand-lighter: #ffffff12;
    background-color: var(--brand-dark);
    font-family: Arial, Helvetica, sans-serif;
    color: white;
}

.container{
    display: flex;
    align-items: center;
    justify-content: center;
    width: 100%;
    padding: 5vw 0;
}
  
.form{
    display: flex;
    flex-direction: column;
    gap: 25px;
    border: 1px solid var(--brand-light);
    border-radius: 16px;
    padding: 40px;
    width: 465px;
    min-width: 22vw;
    background-color: var(--brand-lighter);
}

.button{
    min-width: 100px;
    max-width: 182px;
    width: 19vw;
    background-color: var(--brand-light);
    color: var(--brand-dark);
    border: none;
    border-radius: 16px;
    padding: 8px 26px;
    display: block;
    font-size: 1.2rem;
    margin: auto;
}

.errors{
    display: flex;
    flex-direction: column;
    gap: 10px;
    height: fit-content;
    min-height: 91px;
}

</style> 