<template>
  <main id="landing" class="page-container">
    <div class="banner-container">
      <div class="logo-wrapper">
        <div class="logo-container">
          <h2>COSCUP 2024</h2>
          <div class="logo-content">
            <img src="../assets/images/banner-logo.svg" alt="COSCUP" />
            <div>
              <p>Conference for Open Source Coders, Users & Promoters</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <section class="info-block">

      <div class="info">
        <div class="row">
          <div class="icon">
            <icon-akar-icons-calendar></icon-akar-icons-calendar>
          </div>
          <span>{{startDate}} ~ {{endDate}}</span>
        </div>
        <div class="row">
          <div class="icon">
            <icon-akar-icons-location></icon-akar-icons-location>
          </div>
          <span>{{ t('landing.info.location') }}</span>
        </div>
      </div>
    </section>
    <section class="links">
      <a href="https://blog.coscup.org/2024/02/coscup-2024-early-bird-call-for.html" target="_blank" rel="noopener noreferrer">
        {{ t('landing.links.cfp') }}
      </a>
      <a href="https://blog.coscup.org/2024/02/blog-post.html" target="_blank" rel="noopener noreferrer">
        {{ t('landing.links.community') }}
      </a>
      <a href="https://volunteer.coscup.org/" target="_blank" rel="noopener noreferrer">
        {{ t('landing.links.volunteer') }}
      </a>
      <!-- <router-link to="sponsorship">
        {{ t('landing.links.sponsor') }}
      </router-link> -->
      <a href="https://i.coscup.org/indCfS/" target="_blank" rel="noopener noreferrer">
        {{ t('landing.links.donate') }}
        <p class="codepecker-tip">{{ t('landing.links.donate_tip.codepecker') }}</p>
        <div class="line-one"></div>
        <img class="codepecker" src="@/assets/images/codepecker.png" />
      </a>
    </section>
    <section class="media-links">
      <a
        v-for="media in communityMedia"
        :href="media.link"
        :key="`media-${media.name}`"
        class="media-link"
        target="_blank"
        rel="noopener"
      >
        <component :is="media.icon"></component>
      </a>
    </section>
    <section :key="`section-${section.name}`" class="section-block">
      <img class="prefix-icon" src="@/assets/images/logo.svg" />
      <h2 class="section-title">{{ section.title }}</h2>
      <article class="section-content notice markdown" v-html="section.content"></article>
    </section>
  </main>
</template>

<script lang="ts">
import { defineComponent, ref, watch } from 'vue'
import markdown from '@/utils/markdown'
import IconIg from '~icons/fa-brands/instagram'
import IconBlogger from '~icons/fa-brands/blogger'
import IconFacebook from '~icons/fa-brands/facebook'
import IconFlickr from '~icons/fa-brands/flickr'
import IconPlurk from '~icons/el/plurk-alt'
import IconTwitter from '~icons/fa-brands/twitter'
import IconYoutube from '~icons/fa-brands/youtube'
import IconTelegram from '~icons/fa-brands/telegram-plane'
import IconBullhorn from '~icons/fa-solid/bullhorn'
import IconMedium from '~icons/fa-brands/medium'
import '@/assets/scss/pages/landing.scss'
import { useI18n } from 'vue-i18n'

interface Section {
  name: 'about';
  title: string;
  content: string;
}

const communityMedia = [
  {
    name: 'instagram',
    icon: IconIg,
    link: 'https://www.instagram.com/coscup.tw/'
  },
  {
    name: 'blogger',
    icon: IconBlogger,
    link: 'https://blog.coscup.org/'
  },
  {
    name: 'facebook',
    icon: IconFacebook,
    link: 'https://www.facebook.com/coscup/'
  },
  {
    name: 'flickr',
    icon: IconFlickr,
    link: 'https://www.flickr.com/photos/coscup/'
  },
  {
    name: 'plurk',
    icon: IconPlurk,
    link: 'https://www.plurk.com/coscup'
  },
  {
    name: 'twitter',
    icon: IconTwitter,
    link: 'https://twitter.com/coscup'
  },
  {
    name: 'youtube',
    icon: IconYoutube,
    link: 'https://www.youtube.com/user/thecoscup'
  },
  {
    name: 'telegram',
    icon: IconTelegram,
    link: 'https://t.me/coscupchat'
  },
  {
    name: 'channel',
    icon: IconBullhorn,
    link: 'https://t.me/coscup'
  },
  {
    name: 'medium',
    icon: IconMedium,
    link: 'https://coscup.medium.com'
  }
]

export default defineComponent({
  name: 'Home',
  setup () {
    const { t, locale } = useI18n()
    const section = ref<Section>({ name: 'about', title: '', content: '' })
    const startDate = import.meta.env.VITE_START_DATE
    const endDate = import.meta.env.VITE_END_DATE

    watch(locale, async () => {
      section.value =
      {
        name: 'about',
        title: t('landing.about.title'),
        content: markdown(t('landing.about.content'))
      }
    }, {
      immediate: true
    })

    return {
      t,
      section,
      communityMedia,
      startDate,
      endDate
    }
  }
})
</script>
