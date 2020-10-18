<template>
  <div class="form-container">
    <span class="name">{{ name }}</span>
    <input
      type="text"
      :placeholder="placeholder"
      :value="value"
      @input="$emit('input', $event.target.value)"
    />
    <span class="error">{{ error }}</span>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    placeholder: String,
    value: String,
    error: String,
  },
};
</script> 