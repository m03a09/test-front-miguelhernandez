<template>
  <h1 class="pb-3">Table Avatars</h1>
  <div class="grid grid-cols-5 gap-4 border border-black">
    <div>
      Count
    </div>
    <div>
      UserLogin
    </div>
    <div>
      UserId
    </div>
    <div>
      Site web
    </div>
    <div>
      Avatar
    </div>
  </div>
  <div v-for="(avatar, index) in avatars" class="grid grid-cols-5 gap-4 h-10">
    <div>
      {{ index + 1 }}
    </div>
    <div>
      {{ avatar.login }}
    </div>
    <div>
      {{ avatar.id }}
    </div>
    <div>
      <a :href="avatar.html_url" target="_blank">Profile</a>
    </div>
    <div class="flex items-center justify-center"> <!-- Agrega las clases aquí -->
      <img :src="avatar.avatar_url" class="h-10">
    </div>
  </div>
</template>


<script>
export default {
  name: "TableAvatar",
  props: {
    avatars: {
      type: Array,
      default: []
    }
  }
}
</script>

