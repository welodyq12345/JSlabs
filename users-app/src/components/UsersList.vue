<script setup lang="ts">
import { ref, computed } from 'vue'
import UserCard from './UserCard.vue'

interface User {
  firstName: string
  lastName: string
  gender: 'male' | 'female'
  age: number
  position: string
  photo: string
  hobbies: string[]
}

const users = ref<User[]>([
  {
    firstName: 'Олег',
    lastName: 'Коваль',
    gender: 'male',
    age: 25,
    position: 'Розробник',
    photo: 'https://randomuser.me/api/portraits/men/32.jpg',
    hobbies: ['Футбол', 'Читання', 'Програмування']
  },
  {
    firstName: 'Анна',
    lastName: 'Шевченко',
    gender: 'female',
    age: 17,
    position: 'Дизайнер',
    photo: 'https://randomuser.me/api/portraits/women/44.jpg',
    hobbies: ['Малювання', 'Йога']
  },
  {
    firstName: 'Максим',
    lastName: 'Петренко',
    gender: 'male',
    age: 30,
    position: 'Менеджер',
    photo: 'https://randomuser.me/api/portraits/men/45.jpg',
    hobbies: ['Подорожі', 'Фотографія']
  },
  {
    firstName: 'Софія',
    lastName: 'Бойко',
    gender: 'female',
    age: 22,
    position: 'Тестувальник',
    photo: 'https://randomuser.me/api/portraits/women/68.jpg',
    hobbies: ['Танці', 'Кулінарія', 'Кіно']
  },
  {
    firstName: 'Іван',
    lastName: 'Кравець',
    gender: 'male',
    age: 19,
    position: 'Студент',
    photo: 'https://randomuser.me/api/portraits/men/12.jpg',
    hobbies: ['Геймінг', 'Музика']
  },
  {
    firstName: 'Марія',
    lastName: 'Лисенко',
    gender: 'female',
    age: 28,
    position: 'HR',
    photo: 'https://randomuser.me/api/portraits/women/23.jpg',
    hobbies: ['Читання', 'Волонтерство']
  },
  {
    firstName: 'Дмитро',
    lastName: 'Савченко',
    gender: 'male',
    age: 35,
    position: 'Архітектор',
    photo: 'https://randomuser.me/api/portraits/men/56.jpg',
    hobbies: ['Архітектура', 'Велосипед']
  },
  {
    firstName: 'Олена',
    lastName: 'Мельник',
    gender: 'female',
    age: 16,
    position: 'Школярка',
    photo: 'https://randomuser.me/api/portraits/women/90.jpg',
    hobbies: ['Малювання', 'Танці']
  },
  {
    firstName: 'Павло',
    lastName: 'Ткач',
    gender: 'male',
    age: 40,
    position: 'Директор',
    photo: 'https://randomuser.me/api/portraits/men/78.jpg',
    hobbies: ['Гольф', 'Бізнес']
  },
  {
    firstName: 'Юлія',
    lastName: 'Гончар',
    gender: 'female',
    age: 27,
    position: 'Маркетолог',
    photo: 'https://randomuser.me/api/portraits/women/55.jpg',
    hobbies: ['Соціальні мережі', 'Подкасти']
  }
])

const filter = ref<'all' | 'male' | 'female'>('all')

// Обчислювана властивість: Повертає відфільтрований масив користувачів.
const filteredUsers = computed(() => {
  if (filter.value === 'all') return users.value
  return users.value.filter(u => u.gender === filter.value)
})
</script>

<template>
  <div class="users-container">
    <div class="toolbar">
      <button
          @click="filter = 'all'"
          :class="{ active: filter === 'all' }"
      >
        Всі
      </button>
      <button
          @click="filter = 'male'"
          :class="{ active: filter === 'male' }"
      >
        Чоловіки
      </button>
      <button
          @click="filter = 'female'"
          :class="{ active: filter === 'female' }"
      >
        Жінки
      </button>
    </div>

    <div class="grid">
      <UserCard
          v-for="user in filteredUsers"
          :key="user.firstName + user.lastName"
          :user="user"
      />
    </div>

    <p v-if="filteredUsers.length === 0" class="empty-message">
      Список юзерів пустий
    </p>
  </div>
</template>

<style scoped>
.users-container {
  padding: 20px;
  max-width: 1400px;
  margin: 0 auto;
}

.toolbar {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-bottom: 30px;
  flex-wrap: wrap;
}

.toolbar button {
  padding: 10px 20px;
  border: 2px solid #1976d2;
  background: white;
  color: #1976d2;
  font-weight: 600;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.3s;
}

.toolbar button:hover {
  background: #1976d2;
  color: white;
}

.toolbar button.active {
  background: #1976d2;
  color: white;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 24px;
  padding: 0 10px;
}

.empty-message {
  text-align: center;
  font-size: 1.4em;
  color: #999;
  margin-top: 50px;
  font-style: italic;
}
</style>