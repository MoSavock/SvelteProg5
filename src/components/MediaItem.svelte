<script>
	export let info = {}
	$: type = info.Type
	$: title = info.Title ? info.Title : "N/A"
	$: imdbid = info.imdbID
	$: year = info.Year ? parseInt(info.Year) : "N/A"
	$: imdb_link = `https://www.imdb.com/title/${info.imdbID}`
	$: full_title = info.Title ? `${info.Title} (${info.Year})` : "N/A"
	$: poster = info.Poster !== "N/A" ? info.Poster : "/img/placeholder.jpg"
	import { createEventDispatcher } from 'svelte'
	const dispatch = createEventDispatcher()
	const showModal = async () => { dispatch('showModal', {id: imdbid}) }
</script>

<style lang="sass">
.media-item
	flex: 1
	color: white
	margin: 0.5rem
	min-width: 100%
	background: #eee
	display: flex
	flex-wrap: wrap
	align-items: center
	justify-content: center
	animation: fadeIn 0.2s ease-in-out
	border-radius: 0.5rem
	text-decoration: none
	transition: box-shadow 0.25s ease-in-out
	box-shadow: 0 0 0.5rem 0.15rem rgba(black, 0.15)
	&:hover
		box-shadow: 0 0 0.5rem 0.33rem rgba(black, 0.15)
	@media (min-width: 35rem)
		min-width: 40%
		max-width: 50%
	@media (min-width: 56rem)
		min-width: 30%
	.media-item-title
		padding: 1rem
		min-width: 100%
		font-size: 1.5rem
		text-align: center
		line-height: 1.5rem
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
	.media-item-poster-wrapper
		width: auto
		margin: 1.5rem
		min-height: 250px
		@media (max-width: 55rem)
			width: 100%
		.media-item-poster
			height: 250px
			margin: 0 auto
			padding: 0.5rem
			max-width: 100%
			background: rgba(white, 0.5)
			display: flex
			flex-wrap: wrap
			align-items: center
			justify-content: center
			box-sizing: content-box
			border-radius: 0.25rem
			box-shadow: 0 0 0.5rem 0.15rem rgba(black, 0.15)
	.media-item-actions
		width: 100%
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		justify-content: space-between
		.media-item-action
			padding: 0.5rem
			margin: 0.5rem
			cursor: pointer
			display: flex
			flex-wrap: wrap
			align-items: center
			justify-content: center
			border-radius: 0.25rem
			transition: all 0.2s ease-in-out
			box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
			&:hover
				box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.15), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.25) inset
			.media-item-action-icon
				height: 2rem
				width: auto
			.media-item-action-text
				padding: 0.25rem
				font-size: 0.9rem
				line-height: 0.9rem
</style>

<div class="media-item" data-imdbid="imdbid">
	<p class="media-item-title">{full_title}</p>
	<div class="media-item-poster-wrapper">
		<img class="media-item-poster" src={poster} alt={`Poster for ${title}`}>
	</div>
	<div class="media-item-actions">
		<div class="media-item-action" on:click={showModal}>
			<img class="media-item-action-icon" src="/icons/more.svg" alt="Show more">
			<p class="media-item-action-text">Details</p>
		</div>
		<a class="media-item-action" href={imdb_link} target="_blank">
			<img class="media-item-action-icon" src="/icons/imdb.svg" alt="Go to IMDb">
		</a>
	</div>
</div>
