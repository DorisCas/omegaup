<template>
  <span class="grader-count badge" v-bind:class="graderBadgeClass">{{
    graderCounter
  }}</span>
</template>

<style>
.grader-error {
  color: #b94a48;
  background-image: linear-gradient(
    rgb(242, 222, 222) 0px,
    rgb(231, 195, 195) 100%
  );
  background-color: rgb(242, 222, 222);
}

.grader-ok {
  color: #468847;
  background-image: linear-gradient(
    rgb(223, 240, 216) 0px,
    rgb(200, 229, 188) 100%
  );
  background-color: rgb(223, 240, 216);
}

.grader-warning {
  color: #c09853;
  background-image: linear-gradient(to bottom, #fcf8e3 0, #f8efc0 100%);
  border-color: #f5e79e;
}
</style>

<script lang="ts">
import { Vue, Component, Prop } from 'vue-property-decorator';
import { T } from '../../omegaup.js';
import UI from '../../ui.js';
import omegaup from '../../api.js';

@Component({})
export default class GraderCountBadge extends Vue {
  @Prop() queueLength!: number;
  @Prop() error!: boolean;

  get graderCounter(): string {
    if (this.error === true) {
      return '?';
    } else if (this.queueLength === -1) {
      return '…';
    }
    return `${this.queueLength}`;
  }

  get graderBadgeClass(): string {
    if (this.queueLength === -1 && this.error === false) {
      return '';
    } else if (this.error === true) {
      return 'grader-error';
    } else if (this.queueLength < 5) {
      return 'grader-ok';
    }
    return 'grader-warning';
  }
}
</script>
