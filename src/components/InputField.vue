<template>
  <div class="mb-4">
    <label class="block lg:font-bold font-semibold mb-2" :for="label">{{
      label
    }}</label>
    <input
      :id="label"
      v-model.trim="localValue"
      @input="validateInput"
      :placeholder="placeholder"
      class="w-full border border-gray-300 rounded py-2 px-4 focus:outline-none focus:ring-2 focus:ring-blue-500 cursor-pointer text-black"
    />
    <div v-if="errors.length" class="text-red-500 mt-1">
      <div v-for="error in errors" :key="error">{{ error }}</div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: String,
    modelValue: String,
    placeholder: String,
    rules: Array,
  },
  data() {
    return {
      localValue: this.modelValue,
      errors: [],
    };
  },
  methods: {
    validateInput() {
      this.$emit("update:modelValue", this.localValue);
      this.errors = [];
      this.rules.forEach((rule) => {
        const result = rule(this.localValue);
        if (typeof result === "string") {
          this.errors.push(result);
        }
      });
      this.$emit("inputErrors", {
        field: this.label.toLowerCase(),
        errors: this.errors,
      });
    },
  },
  watch: {
    modelValue(value) {
      this.localValue = value;
    },
  },
};
</script>
