<script>
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	const search = async () => { dispatch('search') }
</script>

<style lang="sass">
#search
	top: 0
	left: 0
	right: 0
	z-index: 5
	width: 100%
	margin: 0 auto
	position: fixed
	max-width: 90rem
	background: #eee
	display: flex
	flex-wrap: wrap
	align-items: center
	justify-content: center
	border-radius: 0 0 0.25rem 0.25rem
	transition: all 0.25s ease-in-out
	box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
	#search-text
		width: 10rem
		font-size: 1.25rem
		margin: 0.5rem
		padding: 0.25rem
		border-radius: 0.25rem
		border: 0rem solid rgba(white, 0)
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.025), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
	#search-year
		margin: 0.5rem
		font-size: 1.25rem
		padding: 0.25rem
		border-radius: 0.25rem
		border: 0rem solid rgba(white, 0)
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.025), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
	#search-icon-wrapper
		cursor: pointer
		margin-left: 0.5rem
		border-radius: 0.25rem
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
		&:hover
			#search-icon
				transform: scale(1.25)
		#search-icon
			width: 1.5rem
			height: 1.5rem
			padding: 0.33rem 0.5rem
			box-sizing: content-box
			transition: transform 0.1s ease-in-out
</style>

<div id="search">
	<input id="search-text" type="text" name="search" placeholder="Search...">
	<input id="search-year" type="number" name="year" min="1894" max="2020" placeholder="2020">
	<div id="search-icon-wrapper" on:click={search}>
		<img id="search-icon" src="/icons/search.svg" alt="search">
	</div>
</div>
