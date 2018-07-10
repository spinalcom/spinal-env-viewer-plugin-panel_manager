<script>
import Vue from "vue";
import PanelManager from "./PanelManager";
import panel from "./panel.vue";

const globalType = typeof window === "undefined" ? global : window;
const spinalSystem = globalType.spinal.spinalSystem;

const ClassName = "PanelManager";

const classExtention = class {
  constructor(viewer, options) {
    Autodesk.Viewing.Extension.call(this, viewer, options);
    this.viewer = viewer;
    this.panelManager = new PanelManager(viewer, panel);
  }
  load() {
    globalType.spinal.panelManager = this.panelManager;
    return true;
  }

  unload() {
    return true;
  }
};
export default new class {
  constructor() {
    Autodesk.Viewing.theExtensionManager.registerExtension(
      ClassName,
      classExtention
    ); // this is the register of your class
    window.spinal.ForgeExtentionManager.addExtention(ClassName);
  }
}();
</script>




