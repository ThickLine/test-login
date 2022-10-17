<template>
    <div>
        <div class="relative h-10 input-component mb-5 flex items-center">
            <label :for="formType"
                   v-show="inPutValue"
                   class="absolute left-1 bottom-7 z-5 ransition-all bg-white px-1">
                {{ label }}
            </label>
            <input :type="formType"
                   @input="handleChange"
                   class="form-control block w-full px-3 py-1.5 text-sm text-gray-medium font-normal text-white bg-white bg-clip-padding border-2 border-solid border-gray rounded transition ease-in-out m-0 focus:text-gray-700 focus:bg-white focus:border-gray-600 focus:outline-none placeholder-override input-override"
                   :placeholder="placeholder" />
            <div v-if="isPassword"
                 class="absolute right-5"
                 @click="togglePassword">
                <EyeOpen v-if="showPassword"
                         size="22" />
                <EyeClosed v-if="!showPassword"
                           size="22" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";
import EyeOpen from "@/components/icons/EyeOpen.vue";
import EyeClosed from "@/components/icons/EyeClosed.vue";

@Component({
    components: {
        EyeOpen,
        EyeClosed,
    },
})
export default class Input extends Vue {

    @Prop() label!: string;
    @Prop({ default: "text" }) type!: string;
    @Prop() placeholder!: string;
    @Prop() disabled!: boolean;
    @Prop({ default: false }) isPassword!: boolean;

    public inPutValue = "";
    public showPassword = true;
    public formType = "text";

    public handleChange(event: any): void {
        this.inPutValue = event.target.value;
        this.$emit("input", this.inPutValue);
    }
    public togglePassword(): void {
        this.showPassword = !this.showPassword;
        this.formType = this.showPassword ? "password" : "text";
    }

    created(): void {
        this.formType = this.type;
    }
}
</script>

<style scoped lang="scss">
@layer utilities {
    .placeholder-override::placeholder {
        font-size: 10px;
        color: #343a40;
        font-weight: 700;
        text-transform: uppercase;
    }
}
</style>
