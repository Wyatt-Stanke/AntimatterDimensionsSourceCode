<script>
import ModalOptionsToggleButton from "@/components/ModalOptionsToggleButton";
import OptionsWrapperModal from "@/components/modals/options/OptionsWrapperModal";

export default {
  name: "AnimationOptionsModal",
  components: {
    ModalOptionsToggleButton,
    OptionsWrapperModal,
  },
  data() {
    return {
      infinityUnlocked: false,
      eternityUnlocked: false,
      dilationUnlocked: false,
      realityUnlocked: false,
      animatedThemeUnlocked: false,
      bigCrunch: false,
      eternity: false,
      dilation: false,
      tachyonParticles: false,
      reality: false,
      background: false
    };
  },
  watch: {
    bigCrunch(newValue) {
      player.options.animations.bigCrunch = newValue;
    },
    eternity(newValue) {
      player.options.animations.eternity = newValue;
    },
    dilation(newValue) {
      player.options.animations.dilation = newValue;
    },
    tachyonParticles(newValue) {
      player.options.animations.tachyonParticles = newValue;
    },
    reality(newValue) {
      player.options.animations.reality = newValue;
    },
    background(newValue) {
      player.options.animations.background = newValue;
    }
  },
  methods: {
    update() {
      const progress = PlayerProgress.current;
      this.infinityUnlocked = progress.isInfinityUnlocked;
      this.eternityUnlocked = progress.isEternityUnlocked;
      this.dilationUnlocked = progress.isRealityUnlocked || !Currency.tachyonParticles.eq(0);
      this.realityUnlocked = progress.isRealityUnlocked;
      this.animatedThemeUnlocked = Theme.animatedThemeUnlocked;

      const options = player.options.animations;
      this.bigCrunch = options.bigCrunch;
      this.eternity = options.eternity;
      this.dilation = options.dilation;
      this.tachyonParticles = options.tachyonParticles;
      this.reality = options.reality;
      this.background = options.background;
    }
  },
};
</script>

<template>
  <OptionsWrapperModal
    class="c-modal-options__large"
    @close="emitClose"
  >
    <div class="c-modal-options__button-container">
      <ModalOptionsToggleButton
        v-if="infinityUnlocked"
        v-model="bigCrunch"
        text="Big crunch:"
      />
      <ModalOptionsToggleButton
        v-if="eternityUnlocked"
        v-model="eternity"
        text="Eternity:"
      />
      <ModalOptionsToggleButton
        v-if="dilationUnlocked"
        v-model="dilation"
        text="Dilation:"
      />
      <ModalOptionsToggleButton
        v-if="dilationUnlocked"
        v-model="tachyonParticles"
        text="Tachyon particles:"
      />
      <ModalOptionsToggleButton
        v-if="realityUnlocked"
        v-model="reality"
        text="Reality:"
      />
      <ModalOptionsToggleButton
        v-if="animatedThemeUnlocked"
        v-model="background"
        onclick="Themes.find(player.options.theme).set();"
        text="Background:"
      />
    </div>
  </OptionsWrapperModal>
</template>