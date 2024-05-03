<template>
  <div class="container mx-auto p-8">
    <h1 class="text-3xl font-bold my-8 text-center text-[#FF0000]">
      Daxon Mail Signature Generator
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
