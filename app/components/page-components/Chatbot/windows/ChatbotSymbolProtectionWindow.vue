<template>
<ModalLayout
  :showControls="false"
  :customControls="true"
  :title="$t('Symbol Protection Preferences')"
>
  <div slot="fixed">
    <Tabs :tabs="tabs" :value="selectedTab" @input="onSelectTabHandler">
    </Tabs>
  </div>
  <validated-form ref="form" slot="content" class="chatbot-symbol-protection__container">
    <transition name='fade' mode="out-in" appear>
      <div v-if="selectedTab === 'general' && symbolProtection">
        <div class="row">
          <div class="small-6 columns">
            <VFormGroup
              :title="$t('Auto Permit')"
              v-model="symbolProtection.general.excluded.level"
              :metadata="metadata.symbol.general.excluded.level"
            />
          </div>
          <div class="small-6 columns">
            <VFormGroup
              :title="$t('Punishment')"
              v-model="symbolProtection.general.punishment.type"
              :metadata="metadata.symbol.general.punishment.type"
            />
          </div>
        </div>
        <VFormGroup
          v-if="symbolProtection.general.punishment.type === 'Timeout'"
          :title="$t('Punishment Duration (Value in Seconds)')"
          v-model="symbolProtection.general.punishment.duration"
          :metadata="metadata.symbol.general.punishment.duration"
        />
        <VFormGroup
          :title="$t('Punishment Response (Line breaks will be ignored)')"
          v-model="symbolProtection.general.message"
          :metadata="metadata.symbol.general.message"
        />
      </div>
      <div v-if="selectedTab === 'advanced'">
        <VFormGroup
          :title="$t('Minimum Amount of Symbols')"
          v-model="symbolProtection.advanced.minimum"
          :metadata="metadata.symbol.advanced.minimum"
        />
        <VFormGroup
          :title="$t('Maximum Amount of Symbols')"
          v-model="symbolProtection.advanced.maximum"
          :metadata="metadata.symbol.advanced.maximum"
        />
        <VFormGroup
          :title="$t('Maximum Percent')"
          v-model="symbolProtection.advanced.percent"
          :metadata="metadata.symbol.advanced.percent"
        />
      </div>
    </transition>
  </validated-form>
  <div slot="controls" class="flex flex--space-between">
    <button
      class="button button--default"
      @click="onResetHandler">
      {{ $t('Reset') }}
    </button>
    <div>
      <button
        class="button button--default"
        @click="onCancelHandler">
        {{ $t('Cancel') }}
      </button>
      <button
        class="button button--action"
        @click="onSaveHandler"
        :disabled="errors.items.length > 0"
      >
        {{ $t("Save") }}
      </button>
    </div>
  </div>
</ModalLayout>
</template>

<script lang="ts" src="./ChatbotSymbolProtectionWindow.vue.ts"></script>

<style <style lang="less" scoped>
.chatbot-symbol-protection__container {
  padding-top: 45px;
}
</style>
