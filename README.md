# Tech Trainee Code Test

## Appendix
```javascript
const moviesJson = require('./movies.json');


//1) (Required) Assigning unique id for each movie sequentially starting from 1 till end of array
// and assigning random rating from 1 to 5 for each movie
moviesJson.forEach(function(item,index){
    item.id=index+1
    item.rating=Math.floor(Math.random()*5)+1
})




class MovieAPI {


	//constructor to initialize the object with given parameter
	constructor(movies) {
		this.movies = movies;
		
	}

	//method for returning the current object
	fetchAllMovies(){
		return this.movies;
	}

	//utility/helper method to sort the movies array in ascending order w.r.t rating
	Returnsortedratingarray(movies){
		const sortedrating= movies.sort(function(a,b){
			return a.rating-b.rating
		})
		return sortedrating

	}

	//2) This method returns array of movies of certain genre if found and prints error message if the genre is not found
	returnMoviesOfCertainGenre(inputgenre){
		const genre=["Comedy","Action","Sci-Fi","Adventure","Drama","Horror","Romance"]
		if(!genre.includes(inputgenre)){
			return "Enter a valid genre present in moviesarray"
		}
		const newmovies=[]
		this.movies.forEach(function(item){
			if(item.genre==inputgenre){
				newmovies.push(item)
			}
		})
		return newmovies
	}

	//3) This method removes movie of the given inputid if found and prints error message if id is not found
	removeMovie(inputid){
		if(inputid<1 || inputid>this.movies[this.movies.length-1].id){
			return "Enter a valid id present in moviesarray"
		}
		const removedmoviearray=this.movies.filter(function(item){
			return item.id!=inputid
		})
		return removedmoviearray
	}

	//4) This method returns movies with subtitle and thumb property filtered out
	moviesWithSubtitleAndThumbFilteredOut(){
		const newarr=this.movies.map(function({subtitle,thumb,...rest}){
			return rest
		})
		return newarr
	}
	
	//5) a)This method sorts movies array in ascending order w.r.t title property
	moviesSortedByName(){
		return this.movies.sort(function(item1,item2){
			item1.title.localeCompare(item2.title)
		})
	}

	//5) b) method for returning movies sorted in descending order w.r.t title property
	moviesSortedByNameDesc(){
		return this.movies.sort(function(item1,item2){
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
			return "Cannot return two top and bottom rating movies"
		}
		
		const sortedrating=this.Returnsortedratingarray(this.movies)

		const ratingarray=new Array(sortedrating[sortedrating.length-1],sortedrating[sortedrating.length-2],sortedrating[0],sortedrating[1])

		return ratingarray


	}

	//7) This method prints three top rated movies
	threeTopRatedMovies(){

		if (this.movies.length<3){
			console.log("Cannot print three top rated movies")
			return 
		}

		const sortedrating=this.Returnsortedratingarray(this.movies)
		
		let len=sortedrating.length

		for(let i=len-1;i>=len-3;i--){
			console.log(sortedrating[i])
		}
		
	}

	//8) This method prints movies from bottom to top rating
	printMoviesBottomToTopRatingSorted(){

		const sortedrating=this.Returnsortedratingarray(this.movies)
		
		sortedrating.forEach(function(item){
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
		obj.id=this.movies[this.movies.length-1].id+1
		obj.rating=Math.floor(Math.random()*5)+1
		this.movies.push(obj)
		
	}

	//10) method which returns a movie if the id is found else prints error message
	returnMovie(id){

		if(id<1 || id>this.movies[this.movies.length-1].id){
			return "Enter a valid id present in moviesarray"
		}

		for(let i=0;i<this.movies.length;i++){
			if(id==this.movies[i].id){
				return this.movies[i]
			}
		}
	}

	//11) method for changing the title of the movie with particular id if found else prints error message
	changeTitle(id,newtitle){

		if(id<1 || id>this.movies[this.movies.length-1].id){
			console.log("Enter a valid id present in moviesarray")
			return 
		}

		this.movies.forEach(function(item){
			if(id==item.id){
				item.title=newtitle
			}
		})
	}


}

const API = new MovieAPI(moviesJson);
const allMovies = API.fetchAllMovies();

//uncomment and execute each method individually

//console.log(allMovies)
//console.log(API.returnMoviesOfCertainGenre("Sci-Fi"))
//console.log(API.removeMovie(10))
//console.log(API.moviesWithSubtitleAndThumbFilteredOut())
//console.log(API.moviesSortedByName())
//console.log(API.moviesSortedByNameDesc())
//console.log(API.twoTopAndBottomRatedMovies())
//API.threeTopRatedMovies()
//API.printMoviesBottomToTopRatingSorted()
/*
API.addObject("Big Buck Bunny tells the story of a giant rabbit with a heart bigger than himself. When one sunny day three rodents rudely harass him, something snaps... and the rabbit ain't no bunny anymore! In the typical cartoon tradition he prepares the nasty rodents a comical revenge.\n\nLicensed under the Creative Commons Attribution license\nhttp://www.bigbuckbunny.org", [
	"http://commondatastorage.googleapis.com/gtv-videos-bucket/sample/BigBuckBunny.mp4"
 ], "By Blender Foundation", "images/BigBuckBunny.jpg", "Big Buck Bunny", "Comedy")
console.log(allMovies)
*/

//console.log(API.returnMovie(4))

/*
API.changeTitle(10,"my own title")
console.log(allMovies)
*/
```

### Uncomment and execute each method individually
I have spent around 1.5-2 hours on this project.