<template>
  <AposInputWrapper
    :field="field"
    :error="effectiveError" :uid="uid"
    :display-options="displayOptions"
    :modifiers="modifiers"
  >
    <template #body>
      <!-- data-apos-schema-area lets all the child areas know that this area is in a schema (which is in a modal)
       and that we should position the z-index of context menus appropriately high -->
      <div
        class="apos-input-wrapper" :class="!next.items.length ? 'apos-is-empty' : null"
        data-apos-schema-area
      >
        <!-- We do not pass docId here because it is solely for
          contextual editing as far as the area editor is concerned. -Tom -->
        <Component
          :is="editorComponent"
          :options="field.options"
          :items="next.items"
          :choices="choices"
          :id="next._id"
          :field-id="field._id"
          :field="field"
          :generation="generation"
          @changed="changed"
        />
      </div>
    </template>
  </AposInputWrapper>
</template>

<script>
import AposInputAreaLogic from '../logic/AposInputArea';
export default {
  name: 'AposInputArea',
  mixins: [ AposInputAreaLogic ]
};
</script>

<style lang="scss" scoped>
  .apos-field--area {
    max-width: $input-max-width;
    .apos-input-wrapper:not(.apos-is-empty) {
      padding: $spacing-base;
      border: 1px solid var(--a-base-8);
      border-radius: var(--a-border-radius);
    }
  }

</style>
