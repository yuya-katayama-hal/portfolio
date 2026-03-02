<script setup lang="ts">
import type { ButtonProps } from '@nuxt/ui'

// --- Hero ---
const heroLinks: ButtonProps[] = [
  {
    label: 'GitHub',
    icon: 'i-simple-icons-github',
    to: 'https://github.com/yuya-katayama-hal',
    target: '_blank',
    color: 'neutral',
    variant: 'subtle',
    size: 'xl'
  },
  {
    label: 'Contact',
    icon: 'i-lucide-mail',
    to: '#contact',
    color: 'primary',
    size: 'xl'
  }
]

// --- Skills ---
interface Skill {
  name: string
  icon: string
  level: 'Expert' | 'Advanced' | 'Intermediate'
  description: string
}

const skillCategories = [
  {
    title: 'Languages',
    skills: [
      { name: 'C++', icon: 'i-simple-icons-cplusplus', level: 'Expert', description: 'テンプレートメタプログラミング、RAII、ムーブセマンティクス' },
      { name: 'C', icon: 'i-simple-icons-c', level: 'Expert', description: '組み込み・システムレベルプログラミング' },
      { name: 'Rust', icon: 'i-simple-icons-rust', level: 'Intermediate', description: 'メモリ安全なシステムプログラミング' },
    ] as Skill[]
  },
  {
    title: 'Tools & Frameworks',
    skills: [
      { name: 'CMake', icon: 'i-simple-icons-cmake', level: 'Expert', description: 'クロスプラットフォームビルド構成、CTest統合' },
      { name: 'Git', icon: 'i-simple-icons-git', level: 'Expert', description: 'ブランチ戦略、サブモジュール管理' },
      { name: 'Linux', icon: 'i-simple-icons-linux', level: 'Intermediate', description: '' },
    ] as Skill[]
  },
  {
    title: 'Specialties',
    skills: [
      { name: 'テスト', icon: 'i-lucide-check-circle', level: 'Advanced', description: 'Boost.Test、Catch2' },
      { name: 'CI/CD', icon: 'i-lucide-git-branch', level: 'Advanced', description: 'GitHub Actions、GitLab CI' },
      { name: 'マルチスレッド', icon: 'i-lucide-cpu', level: 'Intermediate', description: 'std::thread、std::atomic' },
    ] as Skill[]
  }
]

const levelColor = (level: string) => {
  switch (level) {
    case 'Expert': return 'primary'
    case 'Advanced': return 'info'
    case 'Intermediate': return 'neutral'
    default: return 'neutral'
  }
}

// --- Navigation ---
const navLinks = [
  { label: 'About', to: '#about' },
  { label: 'Skills', to: '#skills' },
  { label: 'Contact', to: '#contact' }
]
</script>

<template>
  <div>
    <UApp>
      <!-- Header -->
      <UHeader title="Portfolio">
        <template #right>
          <UButton
            v-for="link in navLinks"
            :key="link.label"
            :label="link.label"
            :to="link.to"
            variant="ghost"
            color="neutral"
          />
          <UColorModeButton />
        </template>
      </UHeader>

      <UMain>
        <!-- Hero Section -->
        <UPageHero
          id="about"
          headline="C++ Engineer"
          title="片山悠哉"
          description="高パフォーマンスなシステムソフトウェアの設計・実装を専門とするC++エンジニアを目指しています。モダンC++の機能を活用し、安全かつ効率的なコードを追求しています。"
          orientation="horizontal"
          :links="heroLinks"
        >
          <div class="flex items-center justify-center">
            <UAvatar
              src="https://avatars.githubusercontent.com/yuya-katayama-hal"
              alt="片山悠哉"
              size="3xl"
              :ui="{ root: 'size-48 text-6xl' }"
            />
          </div>
        </UPageHero>

        <!-- Skills Section -->
        <UPageSection
          id="skills"
          title="Skills"
          description="主要な技術スタックと専門領域"
        >
          <div class="flex flex-col gap-12">
            <div v-for="category in skillCategories" :key="category.title">
              <h3 class="text-lg font-semibold text-highlighted mb-4">
                {{ category.title }}
              </h3>

              <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                <UCard
                  v-for="skill in category.skills"
                  :key="skill.name"
                >
                  <div class="flex items-start gap-4">
                    <UIcon
                      :name="skill.icon"
                      class="size-8 shrink-0 text-primary"
                    />
                    <div class="flex-1 min-w-0">
                      <div class="flex items-center gap-2 mb-1">
                        <span class="font-medium text-highlighted">{{ skill.name }}</span>
                        <UBadge
                          :label="skill.level"
                          :color="levelColor(skill.level)"
                          variant="subtle"
                          size="xs"
                        />
                      </div>
                      <p class="text-sm text-muted">{{ skill.description }}</p>
                    </div>
                  </div>
                </UCard>
              </div>
            </div>
          </div>
        </UPageSection>

        <!-- Contact CTA -->
        <UPageCTA
          id="contact"
          title="Contact"
          variant="subtle"
          :links="[
            { label: 'ths51288@ths.hal.ac.jp', icon: 'i-lucide-mail', to: 'mailto:ths51288@ths.hal.ac.jp', color: 'primary', size: 'xl' },
            { label: 'GitHub', icon: 'i-simple-icons-github', to: 'https://github.com/yuya-katayama-hal', target: '_blank', color: 'neutral', variant: 'subtle', size: 'xl' }
          ]"
        />
      </UMain>

      <!-- Footer -->
      <UFooter>
        <template #left>
          <span class="text-sm text-muted">© {{ new Date().getFullYear() }} Yuya Katayama. All rights reserved.</span>
        </template>
        <template #right>
          <UButton
            icon="i-simple-icons-github"
            to="https://github.com/yuya-katayama-hal"
            target="_blank"
            variant="ghost"
            color="neutral"
          />
        </template>
      </UFooter>
    </UApp>
  </div>
</template>
