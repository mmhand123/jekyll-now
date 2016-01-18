---
layout: post
title: Passing data between Angular controllers
---

## Another way besides using the root scope

Sometimes we want to have access to persistant data between different views. One way to accomplish this is to use the root scope, but it's best to keep this uncluttered. A better way is by using either a service or a factory. For this post, I'm going to describe how to do so using a factory.

First off, let's create our main app:

```javascript
(function() {
  'use strict';
  angular.module('app', [])
    .controller('MainController', MainController);
    
  function MainController () {
    var self = this;
    this.count = 0;
  }
})();

```

This would let us use the count variable anywhere that the MainController is the controller, but what if we wanted to have access to that count variable elsewhere? For that, we could create a factory to store the count data.

```javascript
(function() {
  'use strict';
  angular.module('app.factory', [])
    .factory('DataStore', DataStore);
    
  function DataStore () {
    var count = 0;
    
    return {
      count: count
    };
  }
})();

```

And then update the main app module to be:

```javascript
(function() {
  'use strict';
  angular.module('app', ['app.factory'])
    .controller('MainController', ['DataStore', MainController]);
    
  function MainController (DataStore) {
    var self = this;
    this.count = DataStore.count;
  }
})();

```
Now, whenever the MainController is loaded, it will get set its count variable equal to whatever is in the DataStore factory. This is useful because we can update the datastore from the controller, switch to a view with a different controller, and still have access to the same data. When we switch back to the main controller we will also have access to the changed data again.

Great! Now we're successfully passing data along between controllers via the factory. However, what if we want a change in that factory to trigger a change on the controller?

One way to do that is by broadcasting an event in the factory and watching for it in the controller.

The only thing is that we need a parent scope to broadcast on that the scope of the controller can look back to for the broadcast. For that, we can add the broadcast on the rootscope, which is at the base of all scopes.

```javascript
(function() {
  'use strict';
  angular.module('app.factory', [])
    .factory('DataStore', ['$rootScope', DataStore]);
    
  function DataStore ($rootScope) {
    var count = 0;
    
    var increment = function () {
      this.count++;
      $rootScope.$broadcast('countChange', this.count);
    };
    
    return {
      count: count,
      increment: increment
    };
  }
})();

```

And in the main controller:

```javascript
(function() {
  'use strict';
  angular.module('app', ['app.factory'])
    .controller('MainController', ['DataStore', MainController]);
    
  function MainController (DataStore) {
    var self = this;
    this.count = DataStore.count;
    this.$on('countChange', function(newCount) {
      this.count = DataStore.count;
    });
  }
})();

```
