# Reader-
Angular Front End Application
open with live server

I use live server extension on VsCode ritwickdey.liveserver to open



1. In the view inside the <head> element, include  angular-route.js as a new <script> element.
 <script src="https://code.angularjs.org/1.2.28/angular-route.min.js"></script>


2. In app.js, inject ngRoute into the module’s dependency array so that routing is available for the app to use.
var app = angular.module('ReaderApp', ['ngRoute']);

3. In app.js define app's routes:
use app.config() and $routeProvider 


app.config(function ($routeProvider) {
$routeProvider
.when('/books', {
	controller: 'BookshelfController',
	templateUrl: 'views/book.html'
	})
	 .otherwise({ 
      redirectTo: '/books' 
    })
	});
	
4. Create a service named books for getting data from books API. Create the service in a new file namedjs/services/books.js.
Include this new JavaScript file in the view as a script element <script src="js/services/books.js></script>

app.factory('books', [$http', function($http) {
	return $http.get('https://content.codeacademy.com/courses/ltp4/books-api/books.json')
							.success(function)
				(data) {
							return data;
							})
							.error(function(err)
						{
							return err;
							});
				}]);

5. set up the controller BookshelfController and the template views/bookshelf.html:

1. In the controller BookshelfController , use the books service to load data from the server into the $cope.myBooks
BookshelfContoller.js
app.controller('BookshelfController', ['$scope', 'books', function($scope, books) {

books.success(function(data){
$scope.myBooks = data;
})
}]);

2. Finish the template views/bookshelf.html so that it 

bookshelf.html
<div class="bookshelf row" ng-repeat="book in myBooks">

  <!-- 
  TODO: Loop through myBooks and display each one with this HTML -->
  <div class="book col-md-3">
    <a href="#/books/{{$index}}">
      <img ng-src="{{book.cover}}"/>
      <h3 class="title"> {{ book.title }} </h3>
      <p class="author"> {{ book.author }} </p>
    </a>
  </div>
  

</div>

6. in the view in main section add <div ng-views></div>
<div class="main">
      <div class="container">
        <div ng-view></div>
