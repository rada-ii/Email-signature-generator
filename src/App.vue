<template>
  <div class="container mx-auto sm:p-8 px-2">
    <h1 class="sm:text-3xl text-2xl font-bold my-8 text-center text-[#FF0000]">
      Daxon Email Signature Generator
    </h1>
    <SignatureGenerator />
  </div>
</template>

<script>
import SignatureGenerator from "./components/SignatureGenerator.vue";

export default {
  components: {
    SignatureGenerator,
  },
};
</script>
