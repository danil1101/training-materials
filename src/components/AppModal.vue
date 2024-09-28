<template>
    <div class="modal-mask" v-if="isVisible" @click="handleClickOutside">
        <div class="modal-wrapper">
            <div class="modal-container">
                <div class="modal-header">
                  <div class="title">
                    {{ subject?.title }} - {{ subject?.author }} <span v-if="subject?.subtitle">- {{ subject?.subtitle}}</span>
                  </div>
                  <button class="modal-close" @click="$emit('close')">
                    ×
                  </button>

                </div>


                <div class="modal-body">
                    <iframe :src="subject?.href" frameborder="0"></iframe>
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const emit = defineEmits(['close'])
// eslint-disable-next-line no-unused-vars
const props = defineProps({
    isVisible: Boolean,
    subject: Object
})

const handleClickOutside = (event) => {
    if (event?.target.classList == 'modal-wrapper') {
        emit('close');
    }
}

</script>

<style scoped lang="scss">
.modal-mask {
    position: fixed;
    z-index: 9998;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: table;
}

.modal-wrapper {
    display: table-cell;
    vertical-align: middle;
}

.modal-container {
    width: 100%;
    max-width: 1000px;
    height: 100%;
    max-height: 800px;
    margin: 0px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    position: relative;
    display: flex;
    flex-direction: column;

    @media (max-width: 1000px) {
        min-width: 100%;
        min-height: 100%;

    }
    @media (max-width: 750px) {
        min-width: 100%;
        min-height: 100%;
    }
    @media (max-height: 750px) {
        height: 100dvh;
        min-width: 100%;
        min-height: 100%;

    }
}

.modal-header {
display: flex;
  justify-content: space-between;
  align-items: center;
}

.modal-title {
    font-size: 18px;
    font-weight: 500;
    word-wrap: break-word;
}

.modal-body {
    margin: 20px 0;
    height: 100%;
    display: flex;
    justify-content: center;
    width: 100%;

    @media (max-width: 1000px) {
        margin: 20px auto;
        align-items: center;
    }

    @media (max-width: 540px) {
        margin: 20px 0;
    }

    iframe {
        user-select: none;
        margin: 0 auto;
        width: 540px;
        height: 700px;

        @media (max-width: 540px) {
            width: 100%;
            height: 100%;
        }
    }
}

.modal-close {
    font-size: 50px;
    display: block;
    outline: 0;
    border: 0;
    background: none;
    cursor: pointer;
    transition: all 0.2s ease 0s;
    color: #000;

    &:hover {
        opacity: 0.7;
    }
}
</style>
