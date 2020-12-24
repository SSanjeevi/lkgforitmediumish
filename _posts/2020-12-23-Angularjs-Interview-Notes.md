---
layout: post
title:  "AngularJS Interview Notes"
author: "Sanjeevi Subramani"
categories: [ Angularjs, Interview Notes ]
image: assets/images/12.jpg
featured: true
hidden: true
---
**AngularJS**

- AngularJS is a client-side JavaScript MVC framework to develop a dynamic web application.
- entirely based on HTML and JavaScript
- The ng-app directive is a starting point of AngularJS Application. It initializes the AngularJS framework automatically. AngularJS framework will first check for ng-app directive in a HTML document after the entire document is loaded and if ng-app is found, it bootstraps itself and compiles the HTML template.
- \&lt;bodyng-app=&quot;myAngularApp&quot;\&gt;

\&lt;script\&gt;

var app = angular.module(&#39;myAngularApp&#39;, []);

\&lt;/script\&gt;

- {{ expression }}

  1. Directives

| Directive | Description |
| --- | --- |
| ng-app | Auto bootstrap AngularJS application. |
| --- | --- |
| ng-init | Initializes AngularJS variables |
| ng-model | Binds HTML control&#39;s value to a property on the $scope object. |
| ng-controller | Attaches the controller of MVC to the view. |
| ng-bind | Replaces the value of HTML control with the value of specified AngularJS expression. |
| ng-repeat | Repeats HTML template once per each item in the specified collection. |
| ng-show | Display HTML element based on the value of the specified expression. |
| ng-readonly | Makes HTML element read-only based on the value of the specified expression. |
| ng-disabled | Sets the disable attribute on the HTML element if specified expression evaluates to true. |
| ng-if | Removes or recreates HTML element based on an expression. |
| ng-click | Specifies custom behavior when an element is clicked. |

\&lt;divng-controller=&quot;myController&quot;\&gt;

{{message}}

\&lt;/div\&gt;

\&lt;script\&gt;

var ngApp = angular.module(&#39;myNgApp&#39;, []);

ngApp.controller(&#39;myController&#39;, function ($scope) {

$scope.message = &quot;Hello World!&quot;;

});

\&lt;/script\&gt;

- $scope – inside controller
- $rootscope – overall ngapp

\&lt;bodyng-app=&quot;myNgApp&quot;\&gt;

\&lt;divng-controller=&quot;myController&quot;\&gt;

Enter Message: \&lt;inputtype=&quot;text&quot;ng-model=&quot;message&quot;/\&gt;\&lt;br/\&gt;

\&lt;buttonng-click=&quot;showMsg(message)&quot;\&gt;Show Message\&lt;/button\&gt;

\&lt;/div\&gt;

\&lt;script\&gt;

var ngApp = angular.module(&#39;myNgApp&#39;, []);

ngApp.controller(&#39;myController&#39;, function ($scope) {

$scope.message = &quot;Hello World!&quot;;

$scope.showMsg = function (msg) {

alert(msg);

};

});

\&lt;/script\&gt;

\&lt;/body\&gt;

  1. **Scope object methods:**

The $scope object contains various methods. The following table lists important methods of $scope object.

| Method | Description |
| --- | --- |
| $new() | Creates new child scope. |
| --- | --- |
| $watch() | Register a callback to be executed whenever model property changes. |
| $watchGroup() | Register a callback to be executed whenever model properties changes. Here, specify an array of properties to be tracked. |
| $watchCollection() | Register a callback to be executed whenever model object or array property changes. |
| $digest() | Processes all of the watchers of the current scope and its children.Â  |
| $destroy() | Removes the current scope (and all of its children) from the parent scope. |
| $eval() | Executes the expression on the current scope and returns the result. |
| $apply() | Executes an expression in angular outside the angular framework. |
| $on() | Register a callback for an event. |
| $emit() | Dispatches the specified event upwards till $rootScope. |
| $broadcast() | Dispatches the specified event downwards to all child scopes. |

  1. AngularJS event directives.

| Event Directive |
| --- |
| ng-blur |
| --- |
| ng-change |
| ng-click |
| ng-dblclick |
| ng-focus |
| ng-keydown |
| ng-keyup |
| ng-keypress |
| ng-mousedown |
| ng-mouseenter |
| ng-mouseleave |
| ng-mousemove |
| ng-mouseover |
| ng-mouseup |

  1. built-in AngularJS services.

| $anchorScroll | $exceptionHandler | $interval | $rootScope |
| --- | --- | --- | --- |
| $animate | $filter | $locale | $sceDelegate |
| $cacheFactory | $httpParamSerializer | $location | $sce |
| $templateCache | $httpParamSerializerJQLike | $log | $templateRequest |
| $compile | $http | $parse | $timeout |
| $controller | $httpBackend | $q | $window |
| $document | $interpolate | $rootElement |
 |

    1. **$http is a service as an object. It includes following shortcut methods.**

| Method | Description |
| --- | --- |
| $http.get() | Perform Http GET request. |
| --- | --- |
| $http.head() | Perform Http HEAD request. |
| $http.post() | Perform Http POST request. |
| $http.put() | Perform Http PUT request. |
| $http.delete() | Perform Http DELETE request. |
| $http.jsonp() | Perform Http JSONP request. |
| $http.patch() | Perform Http PATCH request. |

    2. **HTTP:**

var promise = $http.get(&quot;/demo/getdata&quot;).success(onSuccess).error(onError);

$http.post(&#39;/demo/submitData&#39;, { myData: &#39;Hello World!&#39; })

.success(onSuccess)

.error(onError);

    1. **LOG:**

$log.log(&#39;This is log.&#39;);

$log.error(&#39;This is error.&#39;);

$log.info(&#39;This is info.&#39;);

$log.warn(&#39;This is warning.&#39;);

$log.debug(&#39;This is debugging.&#39;);

**9.5. Angularjs filters:**

{{expression | filterName:parameter }}

| Filter Name | Description |
| --- | --- |
| Number | Formats a numeric data as text with comma and fraction. |
| --- | --- |
| Currency | Formats numeric data into specified currency format and fraction. |
| Date | Formats date to string in specified format. |
| Uppercase | Converts string to upper case. |
| Lowercase | Converts string to lower case. |
| Filter | Filters an array based on specified criteria and returns new array. |
| orderBy | Sorts an array based on specified predicate expression. |
| Json | Converts JavaScript object into JSON string |
| limitTo | Returns new array containing specified number of elements from an existing array. |

  1. **Modules:**

Different files:

app.js:

var myApp = angular.module(&quot;myApp&quot;, []);

myController.js:

myApp.controller(&quot;myController&quot;, function ($scope) {

$scope.message = &quot;Hello Angular World!&quot;;

});

  1. **Forms:**

\&lt;form **ng-submit**** =&quot;submitStudnetForm()&quot;**\&gt;

\&lt;labelfor=&quot;firstName&quot;\&gt;First Name: \&lt;/label\&gt;\&lt;br/\&gt;

\&lt;inputtype=&quot;text&quot;id=&quot;firstName&quot;ng-model=&quot;student.firstName&quot;/\&gt;\&lt;br/\&gt;

\&lt;labelfor=&quot;gender&quot;\&gt;Gender\&lt;/label\&gt;\&lt;br/\&gt;

\&lt;selectid=&quot;gender&quot;ng-model=&quot;student.gender&quot;\&gt;

\&lt;optionvalue=&quot;male&quot;\&gt;Male\&lt;/option\&gt;

\&lt;optionvalue=&quot;female&quot;\&gt;Female\&lt;/option\&gt;

\&lt;/select\&gt;\&lt;br/\&gt;\&lt;br/\&gt;

\&lt;inputtype=&quot;submit&quot;value=&quot;Submit&quot;/\&gt;

\&lt;inputtype=&quot;reset&quot;ng-click=&quot;resetForm()&quot;value=&quot;Reset&quot;/\&gt;

\&lt;/form\&gt;

  1. AngularJS includes the following validation directives.

| Directive | Description |
| --- | --- |
| ng-required | Sets required attribute on an input field. |
| --- | --- |
| ng-minlength | Sets minlength attribute on an input field. |
| ng-maxlength | Sets maxlength attribute on an input field. Setting the attribute to a negative or non-numeric value, allows view values of any length. |
| ng-pattern | Sets pattern validation error key if the ngModel value does not match the specified RegEx expression. |

  1. **Route:**

var app = angular.module(&#39;ngRoutingDemo&#39;, [&#39;ngRoute&#39;]);

app.config(function ($routeProvider) {

$routeProvider.when(&#39;/&#39;, {

templateUrl: &#39;/login.html&#39;,

controller: &#39;loginController&#39;

}).when(&#39;/student/:username&#39;, {

templateUrl: &#39;/student.html&#39;,

controller: &#39;studentController&#39;

}).otherwise({

redirectTo: &quot;/&quot;

});

app.controller(&quot;loginController&quot;, function ($scope, $location) {

$scope.authenticate = function (username) {

// write authentication code here..

$location.path(&#39;/student/&#39; + username)

};

});

app.controller(&quot;studentController&quot;, function ($scope, $routeParams) {

$scope.username = $routeParams.username;

});

  1. **Exception Handling:**

app.config(function ($provide) {

$provide.decorator(&#39;$exceptionHandler&#39;, function ($delegate) {

return function (exception, cause) {

$delegate(exception, cause);

alert(&#39;Error occurred! Please contact admin.&#39;);

};

});

});