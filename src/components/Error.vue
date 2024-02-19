<template>
    <div :class="$style.error">
        <p :class="$style.error__message">{{ message }}</p>
    </div>
  </template>
  
<script>
  export default {
    name: "App",
    props: {
        message: {
            type: String,
            default: ''
        },
    }
  };
  </script>
  
<style module>
.error{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    background-color: rgba(243, 82, 82, 0.22);
    border: 1px solid var(--brand-danger);
    border-radius: 10px;
    padding: 10px 3vw;
    gap: 1vw;
}

.error__message{
    font-size: 1rem;
    padding: 0;
    margin: 0;
    color: var(--brand-danger);
    text-align: center;
}
</style>
  