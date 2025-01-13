<script setup lang="ts">
const route = useRoute()
const id = computed(() => route.params.id as string)

const result = await fetchUser(id.value)
const { data: user, loading } = toRefs(result)

const userSubmissions = ref([])
const userComments = ref([])
fetchUser
watchEffect(async () => {
  if (user.value?.submitted?.slice(0, 10)) {
    userSubmissions.value = await Promise.all(
      user.value.submitted.slice(0, 10).map(id => fetchItem(id))
    )
  }
})

watchEffect(async () => {
  if (user.value?.comments?.slice(0, 10)) {
    userComments.value = await Promise.all(
      user.value.comments.slice(0, 10).map(id => fetchComment(id))
    )
  }
})

useHead({
  title: () => loading.value
    ? 'Loading'
    : user.value
      ? user.value.id
      : 'User not found',
})
</script>

<template>
  <div class="user-view view">
    <LoadingWrapper :loading="loading">
      <template v-if="user">
        <UserCard :user="user" :loading="loading" />
        
        <div class="section-wrapper submissions-section">
          <h2 class="section-title">Recent Submissions</h2>
          <LoadingWrapper :loading="loading">
            <div class="section-content submissions-grid">
              <PostItem
                v-for="submission in userSubmissions"
                :key="submission.id"
                :item="submission"
              />
            </div>
          </LoadingWrapper>
          <div class="view-more">
            <a :href="'https://news.ycombinator.com/submitted?id=' + user.id" target="_blank">
              View all submissions
            </a>
          </div>
        </div>

        <div class="section-wrapper comments-section">
          <h2 class="section-title">Recent Comments</h2>
          <LoadingWrapper :loading="loading">
            <div class="section-content comments-list">
              <PostComment
                v-for="comment in userComments"
                :key="comment.id"
                :comment="comment"
              />
            </div>
          </LoadingWrapper>
          <div class="view-more">
            <a :href="'https://news.ycombinator.com/threads?id=' + user.id" target="_blank">
              View all comments
            </a>
          </div>
        </div>
      </template>
      <template v-else>
        <div class="not-found">
          <h1>User not found.</h1>
        </div>
      </template>
    </LoadingWrapper>
  </div>
</template>

<style lang="postcss">
.user-view {
  max-width: 1200px;
  margin: 0 auto;
  padding: var(--space-lg);
  
  .section-wrapper {
    margin-top: var(--space-xl);
    padding: var(--space-md);
  }
  
  .section-title {
    font-size: 1.25rem;
    font-weight: 600;
    color: var(--text-primary);
    margin-bottom: var(--space-md);
    position: relative;
    padding-bottom: var(--space-sm);
    
    &::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      width: 60px;
      height: 3px;
      background: var(--primary);
      border-radius: var(--radius-sm);
    }
  }
  
  .section-content {
    background: var(--bg-card);
    padding: var(--space-md);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-sm);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    margin-bottom: var(--space-lg);

    &:hover {
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
    }
  }

  .submissions-grid {
    display: grid;
    gap: var(--space-md);
  }
  
  .view-more {
    text-align: center;
    margin-top: var(--space-lg);
    
    a {
      color: var(--primary);
      text-decoration: none;
      font-weight: 500;
      
      &:hover {
        text-decoration: underline;
      }
    }
  }
  
  .not-found {
    text-align: center;
    padding: var(--space-xl);
    color: var(--text-secondary);
  }

  .comments-section {
    margin-top: var(--space-xl);
  }

  .comments-list {
    margin-bottom: var(--space-lg);
    background: var(--bg-card);
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-sm);
    transition: transform 0.2s ease, box-shadow 0.2s ease;

    &:hover {
      transform: translateY(-2px);
      box-shadow: var(--shadow-md);
    }
  }
}

@media (max-width: 768px) {
  .user-view {
    padding: var(--space-md);
    
    .submissions-grid {
      gap: var(--space-sm);
    }
  }
}
</style>
