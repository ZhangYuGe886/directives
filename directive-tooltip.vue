<template>
  <div v-tooltip tip='我测试tooltip显示'>rrrrrrrrrrrrrr</div>
</template>

<script>
export default {
  // 自定义提示指令
  directives: {
    tooltip(el, binding) {
      // 鼠标移入时，将浮沉元素插入到body中
      el.onmouseenter = function () {
        // 创建浮层元素并设置样式
        const vcTooltipDom = document.createElement("div");
        vcTooltipDom.style.cssText = `
              width:120px;
              height:30px;
              line-height:30px;
		          position:absolute;
		          background: #000000;
		          color:#ffffff;
		          font-size:14px;
		          z-index:100000
			`;
        // 设置id方便寻找
        vcTooltipDom.setAttribute("id", "vc-tooltip");
        // 将浮层插入到body中
        document.body.appendChild(vcTooltipDom);
        // 浮层中的文字 通过属性值传递动态的显示文案
        document.getElementById("vc-tooltip").innerHTML =
          // el.innerHTML;
          // 获取属性值tip内容
          el.getAttribute('tip')
      };
      // 鼠标移动时，动态修改浮沉的位置属性
      el.onmousemove = function (e) {
        const vcTooltipDom = document.getElementById("vc-tooltip");
        vcTooltipDom.style.top = e.clientY + 15 + "px";
        vcTooltipDom.style.left = e.clientX + 15 + "px";
      };
      // 鼠标移出时将浮层元素销毁
      el.onmouseleave = function () {
        // 找到浮层元素并移出
        const vcTooltipDom = document.getElementById("vc-tooltip");
        vcTooltipDom && document.body.removeChild(vcTooltipDom);
      };
    },
  },
}
</script>

<style>

</style>>