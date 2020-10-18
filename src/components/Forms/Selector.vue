<template>
  <div class="form-container">
    <span class="name">{{ name }}</span>
    <select @change="$emit('change', $event.target.value)" :value="value">
      <option v-for="(v, i) in options" :key="i" :value="v">
        {{ v }}
      </option>
    </select>
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