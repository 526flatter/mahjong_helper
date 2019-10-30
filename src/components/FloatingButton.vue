<template>
    <button @click.self="$emit('click')">
        <slot/>
    </button>
</template>

<script>
export default {
  name: 'FloatingButton'
}
</script>

<style lang="scss" scoped>
button {
    margin: 5px;
	display: inline-block;
	background-color: #26a69b;/*背景色*/
	color: #FFF;/*文字色*/
	font-size: 1em;/*文字サイズ*/
	line-height: 1;
	text-decoration: none;
	letter-spacing: 0.05em;/*字間*/
	padding: 0.2em 1em;/*ボタン内の余白*/
	border-radius: 3px;/*角の丸み*/
	box-shadow: 0 2px 2px 0 rgba(0,0,0,0.14), 0 1px 5px 0 rgba(0,0,0,0.12), 0 3px 1px -2px rgba(0,0,0,0.2);/*影*/
	-webkit-tap-highlight-color: transparent;
	transition: .3s ease-out;/*変化を緩やかに*/
}
</style>
