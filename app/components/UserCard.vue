<template>
  <div class="user-card" :class="{ 'is-loading': loading }">
    <div class="user-card-header">
      <div class="avatar-container">
        <div class="avatar-placeholder">
          <span>{{ user?.id?.charAt(0).toUpperCase() }}</span>
        </div>
      </div>
      <div class="user-info">
        <h2 class="username">{{ user?.id }}</h2>
        <p class="join-date">joined {{ timeAgo(user?.created_time) }}</p>
      </div>
    </div>
    
    <div class="user-stats">
      <div class="stat-item">
        <span class="stat-value">{{ user?.karma }}</span>
        <span class="stat-label">Karma</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">{{ user?.submitted?.length || 0 }}</span>
        <span class="stat-label">Submissions</span>
      </div>
    </div>

    <div class="user-about" v-if="user?.about">
      <h3>About</h3>
      <p v-html="user.about"></p>
    </div>
  </div>
</template>

<script setup lang="ts">
import { timeAgo } from '~~/app/utils'

interface User {
  id: string
  created: number
  karma: number
  about?: string
  submitted?: number[]
}

interface Props {
  user?: User
  loading?: boolean
}

defineProps<Props>()
</script>

<style scoped>
.user-card {
  background: var(--card-bg, #fff);
  border-radius: var(--radius-lg, 12px);
  padding: var(--space-lg, 1.5rem);
  box-shadow: var(--shadow-sm);
  transition: all 0.3s ease;
  max-width: 100%;
  margin: 0 auto;
}

.user-card:hover {
  transform: translateY(-2px);
  box-shadow: var(--shadow-md);
}

.user-card-header {
  display: flex;
  align-items: center;
  gap: var(--space-md, 1rem);
  margin-bottom: var(--space-lg, 1.5rem);
}

.avatar-container {
  flex-shrink: 0;
}

.avatar-placeholder {
  width: 64px;
  height: 64px;
  background: var(--primary-light);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.5rem;
  font-weight: bold;
  color: var(--primary);
}

.user-info {
  flex-grow: 1;
}

.username {
  font-size: 1.25rem;
  font-weight: 600;
  margin: 0;
  color: var(--text-primary);
}

.join-date {
  color: var(--text-secondary);
  font-size: 0.875rem;
  margin: 0.25rem 0 0;
}

.user-stats {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
  gap: var(--space-md, 1rem);
  margin-bottom: var(--space-lg, 1.5rem);
}

.stat-item {
  background: var(--bg-secondary);
  padding: var(--space-md, 1rem);
  border-radius: var(--radius-sm, 8px);
  text-align: center;
  transition: background-color 0.2s ease;
}

.stat-item:hover {
  background: var(--bg-hover);
}

.stat-value {
  display: block;
  font-size: 1.5rem;
  font-weight: 600;
  color: var(--text-primary);
}

.stat-label {
  font-size: 0.875rem;
  color: var(--text-secondary);
}

.user-about {
  border-top: 1px solid var(--border-color);
  padding-top: var(--space-md, 1rem);
}

.user-about h3 {
  font-size: 1rem;
  margin: 0 0 var(--space-sm, 0.75rem);
  color: var(--text-primary);
}

.user-about p {
  margin: 0;
  color: var(--text-secondary);
  line-height: 1.5;
}

.is-loading {
  opacity: 0.7;
  pointer-events: none;
}

@media (max-width: 640px) {
  .user-card {
    padding: var(--space-md, 1rem);
  }

  .avatar-placeholder {
    width: 48px;
    height: 48px;
    font-size: 1.25rem;
  }

  .username {
    font-size: 1.125rem;
  }

  .user-stats {
    grid-template-columns: 1fr 1fr;
  }
}
</style>