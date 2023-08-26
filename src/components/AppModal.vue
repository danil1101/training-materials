<template>
    <div class="modal-mask" v-if="isVisible" @click="handleClickOutside">
        <div class="modal-wrapper">
            <div class="modal-container">
                <button class="modal-default-button" @click="$emit('close')">
                    ×
                </button>
                <div class="modal-header">
                    {{ subject?.title }} - {{ subject?.author }} <span v-if="subject?.subtitle">- {{ subject?.subtitle}}</span>
                </div>

                <div class="modal-body">
                    <iframe :src="subject?.href" frameborder="0"></iframe>
                </div>

            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, watch, defineEmits } from 'vue'

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

watch(()=> props.isVisible, ()=> {
    if (props.isVisible) {
        document.body.classList.add('open-modal')
    }
    if (!props.isVisible) {
        document.body.classList.remove('open-modal')
    }
})
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
    width: 100%;
    height: 100%;
    max-height: 800px;
    margin: 0px auto;
    padding: 20px;
    background-color: #fff;
    border-radius: 2px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
    position: relative;

    @media (max-width: 1000px) {
        min-width: 100%;
        min-height: 100%;

    }
    @media (max-height: 850px) {
        min-width: 100%;
        min-height: 100%;

    }
}

.modal-header {
    display: inline-block;
    margin-top: 0;
    font-size: 18px;
    font-weight: 500;
    padding-right: 50px;
    word-wrap: break-word;
}

.modal-body {
    margin: 20px 0;
    height: 100%;
    display: flex;
    justify-content: center;
    width: 100%;

    @media (max-width: 1000px) {
        margin: 0;
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

.modal-default-button {
    position: absolute;
    right: 20px;
    font-size: 50px;
    line-height: 0;
    top: 20px;
    display: block;
    outline: 0;
    border: 0;
    background: none;
    cursor: pointer;
    padding: 10px;
    transition: all 0.2s ease 0s;

    &:hover {
        opacity: 0.7;
    }
}
</style>