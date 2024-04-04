<script setup>
import { ref } from 'vue';
import { defineProps } from 'vue';
import { useI18n } from 'vue-i18n';

const { t } = useI18n();
const props = defineProps(['label', 'name', 'validation', 'type', 'options']);
const inputLabel = ref('');
const value = ref('');
const radioValue = ref('');

const fillLabel = (val) => {
  const found = props.options.find((element) => element.value == val);
  if (found) {
    inputLabel.value = found.label;
    radioValue.value = found.value;
  }
};
</script>

<template>
  <FormKit
    :type="type"
    @input="fillLabel"
    :label="label"
    :name="name"
    :validation="validation"
    :options="options"
    v-model="value"
  />
  <FormKit
    type="hidden"
    :label="label"
    :name="name + '_label'"
    :validation="validation"
    :options="options"
    v-model="inputLabel"
  />

  <div v-if="name.includes('dog_score')">
    <div v-if="radioValue == '1'" class="text">
      {{ $t('message.very_thin_des') }}
    </div>
    <div v-if="radioValue == '3'" class="text">
      {{ $t('message.slightly_underweight_des') }}
    </div>

    <div v-if="radioValue == '5'" class="text">
      {{ $t('message.ideal_des') }}
    </div>

    <div v-if="radioValue == '7'" class="text">
      {{ $t('message.overweight_des') }}
    </div>

    <div v-if="radioValue == '9'" class="text">
      {{ $t('message.obese_des') }}
    </div>
  </div>
</template>
