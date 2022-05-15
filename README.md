# Tech Trainee Code Test
## Appendix:Code
```javascript
const moviesJson = require('./movies.json');
class MovieAPI {
	//constructor to initialize the object with given parameter
	constructor(movies) {
		this.movies = movies;
		const ids=[]
		this.ids=ids
		this.movies.forEach((item)=>{
			item.id=Math.floor((Date.now() * Math.random()) / 1000);
			this.ids.push(item.id)
			item.rating=Math.floor(Math.random()*5)+1
		})	
	}
	//method for returning the current object
	fetchAllMovies(){
		return this.movies;
	}
	fetchMovieIds(){
		return this.ids
	}
	//utility/helper method to sort the movies array in ascending order w.r.t rating
	moviesSortedByRating(movies){
		const sortedrating= movies.sort((a,b)=>{
			return a.rating-b.rating
		})
		return sortedrating
	}
	//utility/helper method to check whether a given id is valid or not
	isValidId(id){
		const validIds=this.fetchMovieIds()
		if(!validIds.includes(id)){
			return false
		}
		return true
	}
	//2) This method returns array of movies of certain genre if found and prints error message if the genre is not found
	returnMoviesOfCertainGenre(inputgenre){
		const genre=["Comedy","Action","Sci-Fi","Adventure","Drama","Horror","Romance"]
		if(!genre.includes(inputgenre)){
			return "Enter a valid genre present in moviesarray"
		}
		const newmovies=[]
		this.movies.forEach((item)=>{
			if(item.genre==inputgenre){
				newmovies.push(item)
			}
		})
		return newmovies
	}
	//3) This method removes movie of the given inputid if found and prints error message if id is not found
	removeMovie(inputid){
		if(!this.isValidId(inputid)){
			return []
		}
		const removedmoviearray=this.movies.filter((item)=>{
			return item.id!=inputid
		})
		return removedmoviearray
	}
	//4) This method returns movies with subtitle and thumb property filtered out
	moviesWithSubtitleAndThumbFilteredOut(){
		const newarr=this.movies.map(({subtitle,thumb,...rest})=>{
			return rest
		})
		return newarr
	}
	//5) a)This method sorts movies array in ascending order w.r.t title property
	moviesSortedByName(){
		return this.movies.sort((item1,item2)=>{
			item1.title.localeCompare(item2.title)
		})
	}
	//5) b) method for returning movies sorted in descending order w.r.t title property
	moviesSortedByNameDesc(){
		return this.movies.sort((item1,item2)=>{
			let str1=item1.title.toLowerCase()
			let str2=item2.title.toUpperCase()
			if(str1<str2)
			return 1
			else if(str1>str2)
			return -1
			else
			return 0
		})
	}
	//6) This method returns array of movies with two top and bottom rating
	twoTopAndBottomRatedMovies(){
		if(this.movies.length<4){
			return []
		}
		const moviesSortedByRating=this.moviesSortedByRating(this.movies)
		const ratingarray=new Array(moviesSortedByRating[moviesSortedByRating.length-1],moviesSortedByRating[moviesSortedByRating.length-2],moviesSortedByRating[0],moviesSortedByRating[1])
		return ratingarray
	}
	//7) This method prints three top rated movies
	threeTopRatedMovies(){
		if (this.movies.length<3){
			return []
		}
		const moviesSortedByRating=this.moviesSortedByRating(this.movies)
		let len=moviesSortedByRating.length
		for(let i=len-1;i>=len-3;i--){
			console.log(moviesSortedByRating[i])
		}	
	}
	//8) This method prints movies from bottom to top rating
	printMoviesBottomToTopRatingSorted(){
		const sortedrating=this.moviesSortedByRating(this.movies)
		sortedrating.forEach((item)=>{
			console.log(item)
		})
	}
	//9) method for adding a movie object to existing movies array
	addObject(description,sources,subtitle,thumb,title,genre){
		let obj={}
		obj.description=description
		obj.sources=sources
		obj.subtitle=subtitle
		obj.thumb=thumb
		obj.title=title
		obj.genre=genre
		obj.id=Math.floor((Date.now() * Math.random()) / 1000)
		obj.rating=Math.floor(Math.random()*5)+1
		this.ids.push(obj.id)
		this.movies.push(obj)
	}
	//10) method which returns a movie if the id is found else prints error message
	returnMovie(id){
		if(!this.isValidId(id)){
			return []
		}
		for(let i=0;i<this.movies.length;i++){
			if(id==this.movies[i].id){
				return this.movies[i]
			}
		}
	}
	//11) method for changing the title of the movie with particular id if found else prints error message
	changeTitle(id,newtitle){
		if(!this.isValidId(id)){
			return []
		}
		this.movies.forEach((item)=>{
			if(id==item.id){
				item.title=newtitle
			}
		})
	}
}

/*
const API = new MovieAPI(moviesJson);
console.log(allMovies)
const ids=API.fetchMovieIds()
console.log(API.removeMovie(ids[0]))
*/

//console.log(API)
//console.log(allMovies)

/*
const API = new MovieAPI(moviesJson);
console.log(API.returnMoviesOfCertainGenre("Sci-Fi"))
*/

/*
const API = new MovieAPI(moviesJson);
console.log(API.moviesWithSubtitleAndThumbFilteredOut())
*/

/*
const API = new MovieAPI(moviesJson);
console.log(API.moviesSortedByName())
*/

/*
const API = new MovieAPI(moviesJson);
console.log(API.moviesSortedByNameDesc())
*/

/*
const API = new MovieAPI(moviesJson);
console.log(API.twoTopAndBottomRatedMovies())
*/

/*
const API = new MovieAPI(moviesJson);
API.threeTopRatedMovies()
*/

/*
const API = new MovieAPI(moviesJson);
API.printMoviesBottomToTopRatingSorted()
*/

/*
const API = new MovieAPI(moviesJson);
API.addObject("Big Buck Bunny tells the story of a giant rabbit with a heart bigger than himself. When one sunny day three rodents rudely harass him, something snaps... and the rabbit ain't no bunny anymore! In the typical cartoon tradition he prepares the nasty rodents a comical revenge.\n\nLicensed under the Creative Commons Attribution license\nhttp://www.bigbuckbunny.org", [
	"http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
 ], "By Blender Foundation", "images/BigBuckBunny.jpg", "Big Buck Bunny", "Comedy")
console.log(allMovies)
*/

/*
const API = new MovieAPI(moviesJson);
const ids=API.fetchMovieIds()
console.log(API.returnMovie(ids[0]))
*/


/*
const API = new MovieAPI(moviesJson);
const ids=API.fetchMovieIds()
API.changeTitle(ids[10],"my own title")
const allMovies=API.fetchAllMovies()
console.log(allMovies)
*/

```
I have spent around 1.5-2 hours on this project.