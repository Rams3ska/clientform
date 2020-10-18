<template>
  <div class="form-container">
    <span class="name">{{ name }}</span>
    <input
      type="date"
      :value="value"
      min="1900-01-01"
      max="2020-01-01"
      @input="$emit('input', $event.target.value)"
    />
    <span class="error">{{ error }}</span>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    options: Array,
    value: String,
    error: String,
  },
};
</script>