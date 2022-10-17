<template>
    <div>
        <label class="checkbox"
               for="checkbox_input">
            <span class="text-gray-medium text-sm"> {{ label }}</span>
            <input type="checkbox"
                   v-model="checked"
                   id="checkbox_input" />
            <div class="checkbox__indicator"></div>
        </label>
    </div>
</template>

<script lang="ts">
import { Component, Prop, VModel, Vue } from "vue-property-decorator";

@Component
export default class Checkbox extends Vue {
    @VModel() checked!: boolean;
    @Prop() label!: string;
}
</script>

<style scoped lang="scss">
$input-color: #fed800;

.checkbox {
    display: block;
    position: relative;
    padding-left: 30px;
    margin-bottom: 1.415em;
    cursor: pointer;

    input {
        display: none;
    }

    &__indicator {
        position: absolute;
        top: 2px;
        left: 0;
        height: 20px;
        width: 20px;
        background: white;
        border: 1px solid $input-color;
        border-radius: 1px;
        transition: 125ms ease-out;

        &:after {
            content: "";
            position: absolute;
            left: 1px;
            top: 9px;
            width: 7px;
            height: 16px;
            transform: scaleX(-1) rotate(135deg);
            transform-origin: left top;
            border-right: 3px solid white;
            border-top: 3px solid white;
            display: none;
        }
    }

    input:checked~.checkbox__indicator {
        background: white;
    }

    input:checked~.checkbox__indicator:after {
        animation: check 125ms;
        border-top: 1px solid $input-color;
        border-right: 3px solid $input-color;
        display: block;
    }
}
</style>
