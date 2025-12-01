<script setup>
import { computed } from 'vue'
// Props for course details
const props = defineProps({
  id: Number,
  title: String,
  chef: String,
  price: Number,
  level: String,
  available: Boolean
})

const priceFormatted = computed(() => {
  return new Intl.NumberFormat('en-ZA', {
    style: 'currency',
    currency: 'ZAR',
    minimumFractionDigits: 2
  }).format(props.price)
})

const emit = defineEmits(['save'])

function handleSave() {
  emit('save', props.id)
}
</script>

<template>
  <div class="course-card">
    <h2>{{ title }}</h2>
    <p><strong>Chef:</strong> {{ chef }}</p>
    <p><strong>Level:</strong> {{ level }}</p>
    <p><strong>Price:</strong> {{ priceFormatted }}</p>
    <p v-if="available" class="available">Available</p>
    <p v-else class="sold-out">Sold Out</p>
    <button :disabled="!available" @click="handleSave">Save to Wishlist</button>
  </div>
</template>

<style scoped>
.course-card {
  background: #fff;
  color: #213547;
  border-radius: 1em;
  box-shadow: 0 2px 16px rgba(100,108,255,0.08);
  padding: 2em;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  transition: transform 0.2s, box-shadow 0.2s;
}
.course-card h2 {
  margin-top: 0;
  margin-bottom: 0.5em;
  font-size: 1.4em;
}
.course-card p {
  margin: 0.3em 0;
}
.available {
  transition: transform 0.2s, box-shadow 0.2s;
  color: #42b883;
  font-weight: bold;
}
.course-card:hover {
  transform: translateY(-4px) scale(1.03);
  box-shadow: 0 4px 24px #646cff33;
}
.sold-out {
  color: #e63946;
  font-weight: bold;
}
.course-card button {
  margin-top: 1em;
  background: #646cff;
  color: #fff;
  border: none;
  padding: 0.6em 1.2em;
  border-radius: 0.5em;
  font-size: 1em;
  cursor: pointer;
  transition: background 0.2s;
}
.course-card button:disabled {
  background: #ccc;
  cursor: not-allowed;
}
.course-card:hover {
  transform: translateY(-4px) scale(1.03);
  box-shadow: 0 4px 24px #646cff33;
}
</style>
