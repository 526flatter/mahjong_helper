<template>
  <transition name="modal" appear>
    <div class="modal modal-overlay" @click.self="$emit('close')">
      <div class="modal-window">
        <div class="modal-content">
          <slot/>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'TileSelector'
}
</script>

<style lang="scss" scoped>
	.modal {
		&.modal-overlay {
			display: flex;
			align-items: center;
			justify-content: center;
			position: fixed;
			z-index: 30;
			top: 0;
			left: 0;
			width: 100%;
			height: 100%;
			background: rgba(0, 0, 0, 0.5);
  	}

		&-window {
			background: #fff;
			border-radius: 4px;
			overflow: hidden;
		}

		&-content {
			padding: 10px 20px;
			max-width: 80%;
			display: flex;
			flex-wrap: wrap;
			align-items: center;
			justify-content: center;
		}
	}
</style>
