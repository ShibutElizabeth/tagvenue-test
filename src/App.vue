<template>
    <div :class="$style.container">
        <div :class="$style.form">
            <URLInput label="New URL (https only)" @checkInput="updateFirstUrl"></URLInput>
            <URLInput label="Confirm URL" @checkInput="updateSecondUrl"></URLInput>
            
            <div :class="$style.errors">
                <Error message="Provided URLs must be the same!" v-show="url1 != url2"></Error>
                <Error message="Provided URL must be a valid https link!" v-show="url1 != url2"></Error>
            </div>
            <button :class="$style.button" @click="submit">Save</button>
        </div>
    </div>
  </template>
  
<script>

import URLInput from "./components/URLInput.vue";
import Error from "./components/Error.vue";
// import { addNewUrl } from "./api";

export default {
    name: "App",
    data() {
        return {
            firstUrl: '',
            secondUrl: ''
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
                console.log('equal')
            } else {
                console.log('error!');
            }
        },
        isInvalidUrl(url) {
            return !url || !url.match(/https:\/\/.*/)?.[0];
        },
        submit() {
            this.checkEquality();
            // clean whitespace from start/end
            // var clean = this.url1.replaceAll(' ', '');

            // addNewUrl(clean).then(function () {
            //     alert('Saved!');
            // });
        },
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