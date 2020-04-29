<template>
  <div class="container">
    <h3>tmux color selector</h3>
    <div class="preview" :style="{ background: color1 }">
      <div class="status_bar" :style="{ background: color2, color: color3 }">
        <span>0:zsh 1:zsh 2:zsh</span>
      </div>
    </div>
    <textarea name="kanso" rows="4" cols="40" v-model="tmuxConfig"></textarea>
    <div class="form-group">
      <label class="col-md-2 control-label">terminal background</label>
      <div class="col-md-10">
        <input class="form-control" v-model="color1" />
      </div>
    </div>
    <div class="form-group">
      <div class="col-md-offset-2 col-md-10">
        <input class="form-control" type="color" v-model="color1" />
      </div>
    </div>
    <div class="color-palette">
      <h3>Status background</h3>
      <div class="palette">
        <div
          class="color-item"
          v-for="color in colors"
          :key="color.id"
          @click="onClick2(color.rgb)"
          :style="{ background: color.rgb }"
        />
      </div>
      <h3>Status foreground</h3>
      <div class="palette">
        <div
          class="color-item"
          v-for="color in colors"
          :key="color.id"
          @click="onClick3(color.rgb)"
          :style="{ background: color.rgb }"
        />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class HelloWorld extends Vue {
  @Prop() private msg!: string;

  color1 = '#000000';
  color2 = '#ffffff';
  color3 = '#000000';
  colors = [
    { name: 'color0', rgb: '#000000' },
    { name: 'color1', rgb: '#800000' },
    { name: 'color2', rgb: '#008000' },
    { name: 'color3', rgb: '#808000' },
    { name: 'color4', rgb: '#000080' },
    { name: 'color5', rgb: '#800080' },
    { name: 'color6', rgb: '#008080' },
    { name: 'color7', rgb: '#c0c0c0' }
  ];

  tmuxConfig = 'set';

  public onClick2(color: string) {
    this.color2 = color;
    this.updateConfig();
  }

  public onClick3(color: string) {
    this.color3 = color;
    this.updateConfig();
  }

  public updateConfig() {
    this.tmuxConfig = this.color2 + this.color3;
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
.preview {
  height: 100px;
  width: 300px;
  position: relative;
  border-color: black;
  border-width: 1px;
  border-style: solid;
}
.status_bar {
  height: 30px;
  width: 284px;
  font-weight: bold;
  font-size: 1.2em;
  text-align: left;
  padding-left: 16px;
  position: absolute;
  bottom: 0;
}
.color-item {
  height: 30px;
  width: 30px;
  border-color: black;
  border-width: 1px;
  border-style: solid;
}
.palette {
  display: flex;
}
</style>
