# Routing
```
EXAMPLES:
// no need for extra .blade.php extension
Route::get('/example', function () {
    return view('index');
});

// In routes/web.php
Route::get('/example', 'ExampleController@index');

// index is a function in ExampleController class
Route::get('/example', [ExampleController::class, 'index']); 

Route::get('/users/{id}', 'UserController@show');
Route::get('/products/{category?}', 'ProductController@index')->where('category', '.*');
Route::get('/images/{path}', 'ImageController@show')->where('path', '.*');
Route::middleware(['auth'])->group(function () {
    // Routes requiring authentication
    Route::get('/dashboard', 'DashboardController@index');
});

//IMPORTANT SYNTAX 
return ('directory.subdirectory') //same as directory/subdirectory
```

# Blade 
```
{{-- This is a comment in Blade --}}

--Sending Data from controller to view
class ExampleController extends Controller
{
	public function index()
	{
		$users = [
			[
				'name' => 'You',
				'age' => 21,
			],
			[
				'name' => 'Me',
				'age' => 22,
			]
		];
		return view(
			'dashboard',
			[
			'usersList' => $users
			]
		);
	}
}
--So in dashboard.blade.php, that page can access the value $usersList
```
- @ is usually accompanied with directives (eg: @if, ,@elseif, @else, @endif), for shortcuts
- {{}} means echo
- you can modify .env variables and reference it in other blade files
```
--Changes in .env
APP_NAME = Newname

--In config files
'function' => env('APP_NAME','Laravel'), //if null, default is Laravel

--In blade files
{{ config('<{filename}.{function}>')}} 
```
- referencing objects
```
{{ $object->property }}
```


## Blade Templates & Layout
## Blade Layout
- Create a folder for layouts/shared, and usually you will have blade files that contains the headers and footers, or whatever that will be duplicated
- **Use case scenario**:
```
--In layout.blade.php
@yield('content') //defines a section that can be filled with content from child view

--In anotherPage.blade.php
@extends('layouts.layout') //copies all the html code into this file
@section('content')
	<p> This is home page. </p> //this html replaces where @yield is
@endsection

--Instead of putting html code in layouts, you can also put layouts in another file
@include('layouts.anotherLayout') //copies all html code into this file in specific section

@extend is more for parent-child relationship, child views will inherit the structure of the parent view
@include is for reusing and embedding content from another view to current view
```