<script>
	import { onMount } from "svelte"
	import Modal from './components/Modal.svelte'
	import Search from './components/Search.svelte'
	import MediaItem from './components/MediaItem.svelte'
	let items = []
	let page = 2
	let query_val = ""
	let year_val = ""
	let scroll_old = 0
	let scroll_new = 0
	let single = {}
	const handleSearch = async () => {
		let next = document.getElementById("next")
		let intro = document.getElementById("intro-wrapper")
		let query = document.getElementById("search-text").value
		query_val = query !== "" ? `&s=${query}` : ""
		let year = document.getElementById("search-year").value
		year_val = year !== "" ? `&y=${year}` : ""
		let none = document.getElementById("none")
		let response = await fetch(`http://www.omdbapi.com/?apikey=4ad2fcf3&${query_val}${year_val}`)
		let jason = await response.json()
		if (jason.Response == "True") {
			items = []
			page = 2
			intro.classList.add("hide")
			none.classList.add("hide")
			next.classList.remove("hide")
			items = jason.Search
			window.scrollTo(0, 0)
		} else {
			intro.classList.add("hide")
			none.classList.remove("hide")
			window.scrollTo(0, 0)
		}
	}
	const load = async () => {
		let next = document.getElementById("next")
		let query = document.getElementById("search-text").value
		query_val = query !== "" ? `&s=${query}` : ""
		let year = document.getElementById("search-year").value
		year_val = year !== "" ? `&y=${year}` : ""
		let response = await fetch(`http://www.omdbapi.com/?apikey=4ad2fcf3&${query_val}${year_val}&page=${page}`)
		let jason = await response.json()
		let end = document.getElementById("end")
		if (jason.Response == "True") {
			next.classList.remove("hide")
			end.classList.add("hide")
			items = items.concat(jason.Search)
			page++
		} else {
			end.classList.remove("hide")
		}
	}
	const modal = async (e) => {
		let modal = document.getElementById("modal-wrapper")
		let response = await fetch(`http://www.omdbapi.com/?apikey=4ad2fcf3&i=${e.detail.id}`)
		let jason = await response.json()
		single = jason
		modal.classList.remove("hide")
	}
	const handleScroll = () => {
		let y = window.scrollY
		scroll_new = y
		let search_wrapper = document.getElementById("search")
		if (scroll_new > scroll_old) {
			search_wrapper.style.top = "-5rem"
			scroll_old = y
		} else if (scroll_new < scroll_old) {
			search_wrapper.style.top = "0rem"
			scroll_old = y
		}
	}
	onMount(async () => {
		let lazyloadImages = document.querySelectorAll('.lazy')
		let lazyloadImagesLength = lazyloadImages.length
		let imageObserver = new IntersectionObserver((entries, observer) => {
			let entriesLength = entries.length
			for (let i = 0; i < entriesLength; i++) {
				if (entries[i].isIntersecting) {
					let image = entries[i].target
					image.src = image.dataset.lazysrc
					image.classList.remove('lazy')
					imageObserver.unobserve(image)
				}
			}
		})
		for (let e = 0; e < lazyloadImagesLength; e++) {
			imageObserver.observe(lazyloadImages[e])
		}
	})
</script>

<style lang="sass">
#wrapper
	margin: 0 auto
	padding: 0.25rem
	margin-top: 3.5rem
	max-width: 90rem
	min-height: 100vh
	animation: fadeIn 0.2s ease-in-out
	#end, #none
		width: 100%
		text-align: center
	#next
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		width: 10rem
		padding: 0.5rem
		cursor: pointer
		background: #e6e6e6
		margin: 2rem auto
		font-size: 1.5rem
		line-height: 1.5rem
		border-radius: 0.25rem
		transition: all 0.25s ease-in-out
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
		&:hover
			box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.15), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.25) inset
	#media-items
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		align-items: stretch
		border-radius: 0.25rem
		padding: 0.5rem
		background: #e6e6e6
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
	#intro-wrapper
		margin: 5rem auto 0 auto
		max-width: 50rem
		padding: 2rem
		border-radius: 0.25rem
		display: flex
		flex-wrap: wrap
		align-items: center
		justify-content: center
		background: #e6e6e6
		box-shadow: 0 0 0.5rem 0.125rem rgba(0, 0, 0, 0.05), 0 0 0.5rem 0.25rem rgba(255, 255, 255, 0.1) inset
		.intro-wrapper-text
			font-size: 2rem
			line-height: 2rem
			display: flex
			flex-wrap: wrap
			align-items: center
			justify-content: center
</style>

<svelte:window on:scroll={handleScroll}/>

<svelte:head>
	<title>Browse the Open Movie Database (OMDb)</title>
	<meta name="description" content="Browse media in the library of the Open Movie Database">
</svelte:head>

<div id="wrapper">
	<div id="intro-wrapper">
		<p class="intro-wrapper-text">Welcome! Use the search box to browse the media in the library of the Open Movie Database (OMDb) and get detailed information.</p>
	</div>
	<Search on:search={handleSearch} />
	{#if items.length}
		<div id="media-items">
			{#each items as item, index}
				<MediaItem on:showModal={modal} info={item} />
			{/each}
		</div>
	{/if}
	<p id="next" class="hide" on:click={load}>{`Page ${page}`}</p>
	<p id="end" class="hide">End of Results</p>
	<p id="none" class="hide">No results found. Try another search.</p>
	<Modal info={single} />
</div>
