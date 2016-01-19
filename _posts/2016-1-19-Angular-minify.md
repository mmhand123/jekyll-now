---
layout: post
title: Creating minification safe Angular files
---

## Two ways of making Angular files safe for minification

Angular can be tricky when you try to concat and minify all of your files together. Writing Angular code without any safeguards against errant minification can lead to your application no longer working without any clue as to why. The good news is that there are a couple of ways to guard against this.

Code not safe for minification might look like this:

```javascript
angular.module('app')
  .controller('AppController', function($scope, someFactory, someService) {
    ...
  });
  
```

When the minification process happens and variables get renamed, the variables passed into the function will no longer necessarily relate to the same variables they are supposed to represent. One way to protect against this is to use the array syntax:

```javascript
angular.module('app')
  .controller('AppController', ['$scope', 'someFactory', 'someService',
  function($scope, someFactory, someService) {
  
  }]);
  
```

A second way is to use the $inject method. With this method, the $inject will make sure that the right renamed variables get injected into the controller.

```javascript
angular.module('app')
  .controller('AppController', AppController);
  AppController.$inject($scope, someFactory, someService);
  
  function AppController ($scope, someFactory, someService) {
    ...
  }
  
```

Whichever strategy you use, make sure your applications are minification safe!
