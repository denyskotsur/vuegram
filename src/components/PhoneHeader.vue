<template>
    <div class="phone-header">
        <img src="https://s3-us-west-2.amazonaws.com/s.cdpn.io/1211695/vue_gram_logo_cp.png" />
        <a class="cancel-cta"
           v-if="step === 2 || step === 3"
           @click="onCancelHandler">
            Cancel
        </a>
        <a class="next-cta"
           v-if="step === 2"
           @click="onNextHandler">
            Next
        </a>
        <a class="next-cta"
           v-if="step === 3"
           @click="onShareHandler">
            Share
        </a>
    </div>
</template>

<script>
export default {
  name: "phone-header",
  props: {
    onCancelHandler: Function,
    onNextHandler: Function,
    onShareHandler: Function,
    step: Number
  }
};
</script>

<style>
</style>