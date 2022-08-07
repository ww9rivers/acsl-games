<script setup lang="ts">
import WelcomeItem from './WelcomeItem.vue';
import WebIcon from './icons/IconWeb.vue';
import WikiIcon from './icons/IconWiki.vue';
import GithubIcon from './icons/IconGithub.vue';
import SupportIcon from './icons/IconSupport.vue';
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <WebIcon />
    </template>
    <template #heading>The ACSL Website</template>

    This game site is not affiliated with ACSL. Click here to their
    <a target="_blank" href="https://www.acsl.org/">official website</a>.
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <WikiIcon />
    </template>
    <template #heading>The ACSL Wiki</template>

    The <a target="_blank" href="https://www.categories.acsl.org/wiki/">ACSL Wiki</a>
    provides a comprehensive guide over the contents covered in ACSL contests.
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <GithubIcon />
    </template>
    <template #heading>Github Repo</template>

    Source of this project is on
    <a href="https://github.com/ww9rivers/acsl-games" target="_blank">Github</a>.
    Feel free to clone it and collaborate!
  </WelcomeItem>

  <WelcomeItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>Support Vue</template>

    This project is built with Vue.js, which is an independent open source project.
    You can help by
    <a target="_blank" href="https://vuejs.org/sponsor/">becoming a sponsor of Vue</a>.
  </WelcomeItem>
</template>
