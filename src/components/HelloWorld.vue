<template>
  <div class="hello">
    <h1 :class="{ active: isActive }">
      {{ msgWithExclamination || "Please insert message" }}
    </h1>
    <input type="text" v-model="msgWithExclamination" />
    <button @click="onClickClearMessage">Clear Message</button>
  </div>
</template>

<script lang="ts">
import { Prop, Watch, Emit, Component, Vue } from "vue-facing-decorator";

@Component({
  name: "HelloWorld",
})
export default class HelloWorld extends Vue {
  @Prop
  msg!: string;

  msgWithExclamination = "";

  @Watch("msgWithExclamination")
  msgWithExclaminationWatcher(newValue: string, oldValue: string) {
    if (newValue) {
      this.isActive = true;
    } else {
      this.isActive = false;
    }
  }

  @Emit
  onClickClearMessage() {
    this.msgWithExclamination = "";
  }

  isActive = false;

  mounted() {
    this.msgWithExclamination = `${this.msg} !!`;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
h1 {
  color: red;
  &.active {
    color: green;
  }
}
</style>
