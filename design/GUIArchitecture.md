Web GUI architecture
====================

Architecturally, the GUI heavily leans on Google's AngularJS framework. Extending the GUI is as simple as creating a new controller (JS) and defining a new view model (Angular-extended HTML).

``maple.js`` is the main entry point for the web GUI. Controllers can be defined inline in ``maple.js``, though generally it's best to keep separate modules in separate ``.js`` files. Likewise, view models are best defined in their own ``.html`` files.

Example: writing a simple extension to show a table of FIB matches

- [Step 1. Declare your controller](#step-1-declare-your-controller)
- [Step 2. Declare your view-model](#step-2-declare-your-view-model)
- [Step 3. Inject your extension into MapleApp](#step-3-inject-your-extension-into-mapleapp)

#####Step 1. Declare your controller:

````js
// simpleFibController.js
mapleControllers.controller(
    'simpleFIBCtrl',
    [ '$scope'
    , '$http'
    , function($scope,$http) {
	 // initial poll
	 $http.get('/v0/fib').success(function(data) {
	     $scope.rules = data;
	 });
	
	 // poll server again should there be an update
	 var source = new EventSource('/event');
	 
	 function poll(msg) {
        $scope.$apply(function () {
            $http.get('/v0/fib').success(function(data) {
                $scope.rules = data;
            });
        });
	};
	 
	source.addEventListener('message', poll, false);
}]);
````

#####Step 2. Declare your view-model:

````html
<!-- simpleFIB.html -->
<div class="container">

<h1>Simple FIB</h1>

<table id="fibTable" class="table table-striped table-condensed">
<thead>
  <tr>
    <th>Switch</th>
    <th>Inport</th>
    <th>Match</th>
  </tr>
</thead>
<tbody>
<tr ng-repeat="rule in rules">
    <td>{{rule.switch}}</td>
    <td>{{rule.inPort}}</td>
    <td>{{rule.match}}</td>
</tr>
</tbody>
</table>
</div>
````

#####Step 3. Inject your extension into MapleApp:

````js
// maple.js
mapleApp.config(['$routeProvider',
  function($routeProvider) {
    $routeProvider.
      when('/simpleFIB', {
        templateUrl: 'simpleFIB.html',
        controller : 'simpleFIBCtrl'
      });
  }]);
````

````html
<!--maple.html-->
<script src="/path/to/your/simpleFIB.js"></script>
````

Now if we ``make install`` the web app, run maple with mininet, and go to ``http://localhost:3000/simpleFIB``, the simpleFIB extension will be displayed.

Note that extensions do not have to conform to the AngularJS philosophy. Extension authors are free to use their own libraries and frameworks as seen fit, and AngularJS need only provide simple entry point to a self-contained extension app.
