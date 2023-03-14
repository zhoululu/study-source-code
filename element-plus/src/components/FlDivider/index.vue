<template>
    <div :class="['fl-divider', `fl-divider--${direction}`]" :style="dividerStyle">
        <div v-if="$slots.default && direction === 'horizonal'" :class="['fl-divider__text', `is-${ contentPosition }`]">
            <slot></slot>
        </div>
    </div>
</template>

<script setup lang="ts">
import type { PropType, CSSProperties } from 'vue'
import { computed } from 'vue'
defineOptions({
    name: 'FlDivider'
})

const props = defineProps({
    direction: {
        type: String as PropType<'horizonal' | 'vertical'>,
        default: 'horizonal'
    },
    contentPosition: {
        type: String as PropType<'left' | 'center' | 'right'>,
        default: 'left'
    },
    borderStyle: {
        type: String as PropType<CSSStyleDeclaration['borderStyle']>,
        default: 'solid'
    }
})

const dividerStyle = computed(() => {
    return {
        '--fl-border-style': props.borderStyle
    } as CSSProperties
})
</script>

<style lang="scss">
.fl-divider {
    position: relative;
}
.fl-divider--horizonal {
    display: block;
    height: 1px;
    width: 100%;
    margin: 24px 0;
    border-top: 1px var(--fl-border-color) var(--fl-border-style);
}
.fl-divider--vertical {
    display: inline-block;
    width: 1px;
    height: 1em;
    margin: 0 8px;
    vertical-align: middle;
    position: relative;
    border-left: 1px var(--fl-border-color) var(--fl-border-style);
}
.fl-divider__text {
    position: absolute;
    padding: 0 20px;
    background-color: var(--fl-bg-color);
    font-weight: 500;
    color: var(--fl-text-color-primary);
    &.is-left {
        left: 20px;
        transform: translateY(-50%);
    }
    &.is-center {
        left: 50%;
        transform: translateX(-50%) translateY(-50%);
    }
    &.is-right {
        right: 20px;
        transform: translateY(-50%);
    }
}
</style>