<template>
    <div class="phone-footer">
        <div class="home-cta">
            <i class="fas fa-home fa-lg"
               @click="goHomeHandler"></i>
        </div>
        <div class="upload-cta">
            <input type="file"
                   name="file"
                   id="file"
                   class="inputfile"
                   @change="onUploadImage"
                   :disabled="step !== 1" />
            <label for="file">
                <i class="far fa-plus-square fa-lg"></i>
            </label>
        </div>
    </div>
</template>
 
<script>
export default {
  name: "phone-footer",
  props: {
    onUploadImage: Function,
    goHomeHandler: Function,
    step: Number
  }
};
</script>


<style>
</style>