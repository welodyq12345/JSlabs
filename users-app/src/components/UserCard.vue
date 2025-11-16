<script setup lang="ts">
import { defineProps } from 'vue'

interface User {
  firstName: string
  lastName: string
  gender: 'male' | 'female'
  age: number
  position: string
  photo: string
  hobbies: string[]
}

const props = defineProps<{
  user: User
}>()
</script>

<template>
  <div
      class="user-card"
      :class="{ adult: props.user.age >= 18, minor: props.user.age < 18 }"
  >
    <img :src="props.user.photo" alt="Photo" class="photo" />
    <div class="info">
      <h3>{{ props.user.firstName }} {{ props.user.lastName }}</h3>
      <p><strong>Посада:</strong> {{ props.user.position }}</p>
      <p><strong>Стать:</strong> {{ props.user.gender === 'male' ? 'Чоловік' : 'Жінка' }}</p>

      <p v-if="props.user.age >= 18">
        <strong>Вік:</strong> {{ props.user.age }}
      </p>

      <div v-if="props.user.hobbies.length" class="hobbies">
        <strong>Хобі:</strong>
        <ul>
          <li v-for="(hobby, index) in props.user.hobbies" :key="index">
            {{ hobby }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.user-card {
  border: 1px solid #ddd;
  border-radius: 12px;
  padding: 16px;
  max-width: 320px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: all 0.3s ease;
  display: flex;
  gap: 16px;
  background: white;
}

.user-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15);
}

.photo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
  flex-shrink: 0;
}

.info {
  flex: 1;
  text-align: left;
}

.info h3 {
  margin: 0 0 8px;
  color: #1a1a1a;
}

.info p {
  margin: 4px 0;
  color: #444;
}

.hobbies ul {
  margin: 8px 0 0;
  padding-left: 20px;
}

.adult {
  border-left: 5px solid #1976d2;
  background: linear-gradient(135deg, #e3f2fd, #bbdefb);
}

.minor {
  border-left: 5px solid #f57c00;
  background: linear-gradient(135deg, #fff3e0, #ffe0b2);
}
</style>