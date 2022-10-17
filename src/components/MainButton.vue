<template>
    <div :style="iconSize">
        <button type="submit"
                :class="color"
                class="inline-block px-6 py-2 border-2 font-medium text-xs leading-tight uppercase rounded hover:bg-black hover:bg-opacity-5 focus:outline-none focus:ring-0 transition duration-150 ease-in-out">
            {{ text }}
        </button>
    </div>
</template>

<script lang="ts">
import ButtonEnum from "@/enums/buttons";
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class MainButton extends Vue {
    @Prop() text!: string;
    @Prop({ default: 32 }) height!: number;
    @Prop() size!: number;
    @Prop({ default: ButtonEnum.white }) type!: ButtonEnum;

    public get color(): string {
        switch (this.type) {
            case ButtonEnum.yellow:
                return "text-gray-dark border-yellow bg-yellow";

            default:
                return "border-white text-white border-2";
        }
    }

    public get iconSize(): { height: string } {
        return {
            height: (this.size ?? this.height) + "px",
        };
    }
}
</script>
