<template>
    <div class="header">
        <div class="header__logo">Training materials <span>online</span></div>
    </div>
</template>

<script setup lang="ts">

</script>

<style scoped lang="scss">
.header {
    padding: 26px 0;
    user-select: none;

    &__logo {
        font-size: 20px;
        font-weight: 800;
        position: relative;
        display: inline-block;

        span {
            top: -15px;
            right: -12px;
            font-size: 14px;
            font-weight: 400;
            position: absolute;
        }
    }

}
</style>