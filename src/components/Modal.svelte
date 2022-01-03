<script>
	const handleClick = (e) => {
		let modal = document.getElementById("modal-wrapper")
		if (e.target.id == "modal-wrapper") {
			modal.classList.add("hide")
		}
	}
	export let info = {
		Title: "Guardians of the Galaxy Vol. 2",
		Year: "2017",
		Rated: "PG-13",
		Released: "05 May 2017",
		Runtime: "136 min",
		Genre: "Action, Adventure, Comedy, Sci-Fi",
		Director: "James Gunn",
		Writer: "James Gunn, Dan Abnett (based on the Marvel comics by), Andy Lanning (based on the Marvel comics by), Steve Englehart (Star-Lord created by), Steve Gan (Star-Lord created by), Jim Starlin (Gamora and Drax created by), Stan Lee (Groot created by), Larry Lieber (Groot created by), Jack Kirby (Groot created by), Bill Mantlo (Rocket Raccoon created by), Keith Giffen (Rocket Raccoon created by), Steve Gerber (Howard the Duck created by), Val Mayerik (Howard the Duck created by)",
		Actors: "Chris Pratt, Zoe Saldana, Dave Bautista, Vin Diesel",
		Plot: "The Guardians struggle to keep together as a team while dealing with their personal family issues, notably Star-Lord's encounter with his father the ambitious celestial being Ego.",
		Language: "English",
		Country: "USA",
		Awards: "Nominated for 1 Oscar. Another 15 wins & 56 nominations.",
		Poster: "https://m.media-amazon.com/images/M/MV5BNjM0NTc0NzItM2FlYS00YzEwLWE0YmUtNTA2ZWIzODc2OTgxXkEyXkFqcGdeQXVyNTgwNzIyNzg@._V1_SX300.jpg",
		Ratings: [
			{
				Source: "Internet Movie Database",
				Value: "7.6/10"
			},
			{
				Source: "Rotten Tomatoes",
				Value: "85%"
			},
			{
				Source: "Metacritic",
				Value: "67/100"
			}
		],
		Metascore: "67",
		imdbRating: "7.6",
		imdbVotes: "545,424",
		imdbID: "tt3896198",
		Type: "movie",
		DVD: "22 Aug 2017",
		BoxOffice: "$389,804,217",
		Production: "Walt Disney Pictures",
		Website: "N/A",
		Response: "True"
	}
	$: plot = info.Plot ? info.Plot : "N/A"
	$: title = info.Title ? info.Title : "N/A"
	$: rated = info.Rated ? info.Rated : "N/A"
	$: genre = info.Genre ? info.Genre : "N/A"
	$: awards = info.Awards ? info.Awards : "N/A"
	$: imdbid = info.imdbID ? info.imdbID : "N/A"
	$: ratings = info.Ratings ? info.Ratings : "N/A"
	$: language = info.Language ? info.Language : "N/A"
	$: year = info.Year ? parseInt(info.Year) : "N/A"
	$: actors = info.Actors ? `Starring: ${info.Actors}` : "N/A"
	$: writer = info.Writer ? `Writer(s): ${info.Writer}` : "N/A"
	$: metascore = (info.Metascore && info.Metascore !== "N/A") ? parseFloat(info.Metascore) : "N/A"
	$: has_metascore = (info.Metascore && info.Metascore !== "N/A") ? true : false
	$: director = info.Director ? `Director: ${info.Director}` : "N/A"
	$: released = info.Released ? `Released: ${info.Released}` : "N/A"
	$: poster = info.Poster !== "N/A" ? info.Poster : "/img/placeholder.jpg"
	$: production = info.Production ? `Production: ${info.Production}` : " Production: N/A"
	$: full_title = info.Title ? `${info.Title} (${info.Year})` : "N/A"
	$: imdblink = info.imdbID ? `https://www.imdb.com/title/${info.imdbID}/` : "N/A"
	$: imdbvotes = {
		formatted: info.imdbVotes ? info.imdbVotes : "N/A",
		unformatted: info.imdbVotes ? parseFloat(info.imdbVotes.replace(/[^0-9]/gi, "")) : "N/A"
	}
	$: boxoffice = {
		formatted: info.BoxOffice ? info.BoxOffice : "N/A",
		unformatted: info.BoxOffice ? parseFloat(info.BoxOffice.replace(/[^0-9.]/gi, "")) : "N/A"
	}
	$: imdbrating = {
		formatted: info.imdbRating ? info.imdbRating : "N/A",
		unformatted: info.imdbRating ? parseFloat(info.imdbRating.replace(/[^0-9.]/gi, "")) : "N/A"
	}
	$: runtime = {
		formatted: info.Runtime ? info.Runtime : "N/A",
		unformatted: info.Runtime ? parseFloat(info.Runtime.replace(/[^0-9]/gi, "")) : "N/A"
	}
</script>

<style lang="sass">
#modal-wrapper
	height: 100vh
	min-width: 100%
	position: fixed
	top: 0
	left: 0
	z-index: 10
	overflow: hidden
	animation: fadeIn 0.2s ease-in-out
	display: flex
	flex-wrap: wrap
	align-items: center
	justify-content: center
	background: rgba(black, 0.75)
	#modal
		color: white
		margin: 1rem
		width: 100%
		background: #eee
		max-width: 90rem
		display: flex
		flex-wrap: wrap
		justify-content: center
		border-radius: 0.5rem
		transition: box-shadow 0.25s ease-in-out
		box-shadow: 0 0 0.5rem 0.15rem rgba(black, 0.15)
		&:hover
			box-shadow: 0 0 0.5rem 0.33rem rgba(black, 0.15)
		.modal-poster-wrapper
			min-width: 100%
			margin: 1.5rem
			display: none
			@media (min-width: 45rem)
				display: block
				min-width: auto
			.modal-poster
				height: 445px
				margin: 0 auto
				max-width: 100%
				display: flex
				flex-wrap: wrap
				align-items: center
				justify-content: center
				box-sizing: content-box
				border-radius: 0.25rem
				border: 0.5rem solid rgba(white, 0.9)
		.modal-info-wrapper
			flex: 1
			display: flex
			flex-wrap: wrap
			flex-direction: column
			.modal-info
				height: auto
				width: 100%
				display: flex
				flex-wrap: wrap
				align-items: center
				justify-content: center
				&.plot
					flex: 1
					margin: 0 auto
					max-width: 50rem
					transition: all 0.25s ease-in-out
					padding: 0.5rem 0.5rem
					@media (min-width: 45rem)
						padding: 2rem 0.5rem
					.modal-info-item
						text-indent: 0.5rem
						font-size: 1.1rem
						line-height: 1.25rem
						@media (min-width: 56rem)
							font-size: 1.5rem
							line-height: 1.75rem
				.modal-info-item
					padding: 0.25rem
					display: flex
					flex-wrap: wrap
					align-items: center
					justify-content: center
					&.title
						margin-bottom: 1.5rem
						font-size: 1.5rem
						line-height: 1.5rem
						@media (min-width: 56rem)
							font-size: 3rem
							line-height: 3rem
					&.short
						margin: 0 0.5rem
						font-size: 0.9rem
						transition: all 0.25s ease-in-out
						@media (min-width: 56rem)
							font-size: 1.1rem
					&.rating-wrapper
						flex: 1
						display: block
						padding: 0
						width: 100%
						height: 1.5rem
						border-radius: 0.5rem
						overflow: hidden
						background: desaturate(red, 66)
						.rating-fill
							height: 100%
							background: desaturate(green, 66)
					&.icon-wrapper
						.icon
							width: 1.5rem
							height: 1.5rem
							margin: 0.5rem
							box-sizing: content-box
							@media (min-width: 45rem)
								width: 2.5rem
								height: 2.5rem
					&.text-wrapper
						min-width: 6rem
						.text
							display: flex
							flex-wrap: wrap
							align-items: center
							justify-content: center
							font-size: 1.25rem
							margin: 0 0.25rem
							&.number
								opacity: 0.5
</style>

<div id="modal-wrapper" class="hide" on:click={handleClick}>
	<div id="modal">
		<div class="modal-poster-wrapper">
			<img class="modal-poster" src={poster} alt="poster">
		</div>
		<div class="modal-info-wrapper">
			<div class="modal-info">
				<div class="modal-info-item title">{full_title}</div>
			</div>
			<div class="modal-info">
				<div class="modal-info-item short">Rated: {rated}</div>
				<div class="modal-info-item short">Duration: {runtime.formatted}</div>
				<div class="modal-info-item short">Genres: {genre}</div>
				<div class="modal-info-item short">Languages: {language}</div>
			</div>
			<div class="modal-info">
				<div class="modal-info-item short">{actors}</div>
			</div>
			<div class="modal-info plot">
				<div class="modal-info-item">{plot}</div>
			</div>
			<div class="modal-info">
				<div class="modal-info-item short">{released}</div>
				<div class="modal-info-item short">{`Box Office: ${boxoffice.formatted}`}</div>
				<div class="modal-info-item short">{director}</div>
				<div class="modal-info-item short">{production}</div>
				<div class="modal-info-item short">{writer}</div>
			</div>
			{#each ratings as rating}
				<div class="modal-info">
					{#if rating.Source == "Internet Movie Database"}
						<div class="modal-info-item icon-wrapper">
							<img class="icon" src="/icons/imdb.svg" alt="Internet Movie Database">
						</div>
						<div class="modal-info-item rating-wrapper">
							<div class="rating-fill" style={`width: ${imdbrating.unformatted * 10}%;`}></div>
						</div>
						<div class="modal-info-item text-wrapper">
							<span class="text">{imdbrating.formatted} / 10</span>
						</div>
					{/if}
					{#if rating.Source == "Metacritic"}
						<div class="modal-info-item icon-wrapper">
							<img class="icon" src="/icons/metacritic.svg" alt="Metacritic">
						</div>
						<div class="modal-info-item rating-wrapper">
							<div class="rating-fill" style={`width: ${metascore}%;`}></div>
						</div>
						<div class="modal-info-item text-wrapper">
							<span class="text">{metascore / 10} / 10</span>
						</div>
					{/if}
					{#if rating.Source == "Rotten Tomatoes"}
						<div class="modal-info-item icon-wrapper">
							<img class="icon" src="/icons/rottentomatoes.svg" alt="Rotten Tomatoes">
						</div>
						<div class="modal-info-item rating-wrapper">
							<div class="rating-fill" style={`width: ${rating.Value};`}></div>
						</div>
						<div class="modal-info-item text-wrapper">
							<span class="text">{`${parseInt(rating.Value.replace("%", "")) / 10} / 10`}</span>
						</div>
					{/if}
				</div>
			{/each}
		</div>
	</div>
</div>
