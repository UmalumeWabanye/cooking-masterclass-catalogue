<script setup>
import CourseCard from './components/CourseCard.vue'
import { ref, computed } from 'vue'

const courses = [
  {
    id: 1,
    title: 'Italian Pasta Mastery',
    chef: 'Chef Mario Rossi',
    price: 59,
    level: 'Beginner',
    available: true
  },
  {
    id: 2,
    title: 'Sushi Artistry',
    chef: 'Chef Yuki Tanaka',
    price: 89,
    level: 'Advanced',
    available: false
  },
  {
    id: 3,
    title: 'French Pastry Essentials',
    chef: 'Chef Luc Moreau',
    price: 75,
    level: 'Intermediate',
    available: true
  }
]

const wishlist = ref([])
const showAvailableOnly = ref(false)
const wishlistAnim = ref(false)

function addToWishlist(courseId) {
  if (!wishlist.value.includes(courseId)) {
    wishlist.value.push(courseId)
    wishlistAnim.value = true
    setTimeout(() => wishlistAnim.value = false, 500)
  }
}

const filteredCourses = computed(() => {
  return showAvailableOnly.value
    ? courses.filter(c => c.available)
    : courses
})

function removeFromWishlist(courseId) {
  wishlist.value = wishlist.value.filter(id => id !== courseId)
}

const wishlistCourses = computed(() => {
  return courses.filter(c => wishlist.value.includes(c.id))
})
</script>


<template>
  <header class="cm-header">
    <h1>Cooking Masterclass</h1>
    <div :class="['wishlist-counter', { animate: wishlistAnim }]">
      Wishlist: <span>{{ wishlist.length }}</span>
    </div>
    <label class="filter-toggle">
      <input type="checkbox" v-model="showAvailableOnly" />
      Show only available classes
    </label>
  </header>
  <main>
    <section class="catalogue-grid">
      <CourseCard
        v-for="course in filteredCourses"
        :key="course.id"
        :id="course.id"
        :title="course.title"
        :chef="course.chef"
        :price="course.price"
        :level="course.level"
        :available="course.available"
        @save="addToWishlist"
      />
    </section>
  </main>
</template>


<style scoped>
.cm-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding-bottom: 2rem;
  border-bottom: 2px solid #646cff;
}
.wishlist-counter {
  font-size: 1.2em;
  background: #f9f9f9;
  color: #213547;
  padding: 0.5em 1em;
  border-radius: 1em;
  box-shadow: 0 2px 8px rgba(100,108,255,0.08);
  transition: box-shadow 0.3s, background 0.3s;
}
.wishlist-counter.animate {
  background: #646cff;
  color: #fff;
  box-shadow: 0 0 16px #646cff99;
}
.filter-toggle {
  font-size: 1em;
  margin-left: 2em;
  display: flex;
  align-items: center;
  gap: 0.5em;
}
.wishlist-counter.animate {
  background: #646cff;
  color: #fff;
  box-shadow: 0 0 16px #646cff99;
}
.filter-toggle {
  font-size: 1em;
  margin-left: 2em;
  display: flex;
  align-items: center;
  gap: 0.5em;
}
.wishlist-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0,0,0,0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}
.wishlist-content {
  background: #fff;
  color: #213547;
  border-radius: 1em;
  box-shadow: 0 2px 24px #646cff33;
  padding: 2em;
  min-width: 320px;
  max-width: 90vw;
  @media (max-width: 600px) {
    .cm-header {
      flex-direction: column;
      gap: 1em;
      text-align: center;
    }
    .catalogue-grid {
      grid-template-columns: 1fr;
    }
  }
}
.wishlist-content h2 {
  margin-top: 0;
}
.wishlist-content ul {
  list-style: none;
  padding: 0;
}
.wishlist-content li {
  margin-bottom: 1em;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.wishlist-content button {
  margin-left: 1em;
  background: #646cff;
  color: #fff;
  border: none;
  padding: 0.4em 1em;
  border-radius: 0.5em;
  font-size: 1em;
  cursor: pointer;
}
.catalogue-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 2rem;
  margin-top: 2rem;
}
.course-card {
  background: #fff;
  color: #213547;
  border-radius: 1em;
  box-shadow: 0 2px 16px rgba(100,108,255,0.08);
  padding: 2em;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
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
  color: #42b883;
  font-weight: bold;
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
@media (max-width: 600px) {
  .cm-header {
    flex-direction: column;
    gap: 1em;
    text-align: center;
  }
  .catalogue-grid {
    grid-template-columns: 1fr;
  }
}
</style>
