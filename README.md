# angular-jonpapa-snippets package

##Standard Snippets

These snippets are based on [Jon Papa's recommended style guide](), and the already made [angular styleguide snippets](https://github.com/jmiazga/angularjs-styleguide-snippets).

These snippets follow as close to the guide as possible. Note, we are using ui-router for the angular routing system with ng-state, and the built-in routing system with ng-route.

### ngcontroller
```javascript
'use strict';

angular
    .module('${1:module}')
    .controller('${2:Controller}', ${2:Controller});

function ${2:Controller}(${3:dependencies}) {
    var vm = this;

    angular.extend(vm, {
      ${4:function}: ${4:function}
    });

    activate();

    function activate() {

    }

    function ${4:function}() {

    }
}
```

### ngservice
```javascript
'use strict';

angular
    .module('${1:module}')
    .factory('${2:Service}', ${2:Service});

function ${2:Service}(${3:dependencies}) {
    this.${4:function} = ${4:function};

    function ${4:function}() {

    }
}
```

### ngfactory
```javascript
'use strict';

angular
    .module('${1:module}')
    .factory('${2:factory}', ${2:factory});

function ${2:factory}(${3:dependencies}) {
    var service = {
        ${4:function}: ${4:function}
    };

    return service;

    function ${4:function}() {

    }
}
```

### ngmodule
```javascript
'use strict';

angular
    .module('${1:module}', [
        '${2:dependencies}'
    ]);
```

### ngdirective
```javascript
'use strict';

angular
    .module('${1:module}')
    .directive('${2:directive}', ${2:directive});

function ${2:directive}() {
    var directive = {
        restrict: '${3:EA}',
        templateUrl: '${4:templateUrl}',
        scope: {
        },
        link: linkFunc,
        controller: ${5:Controller},
        controllerAs: 'vm',
        bindToController: true
    };

    return directive;

    function linkFunc(scope, el, attr, ctrl) {

    }
}  
```

### ngfilter
```javascript
'use strict';

angular
    .module('${1:module}')
    .filter('${2:filter}', ${2:filter});

function ${2:filter}() {
    return ${2:filter}Filter

    function ${2:filter}Filter(${3:params}) {
        return ${3:params};
    }
}
```

### ngroute
```javascript
'use strict';

angular
  .module('${1:module}')
  .config(config);

function config($routeProvider) {
    $routeProvider
        .when('/${2:route}', {
            templateUrl: '${3:templateUrl}',
            controller: '${4.controller}Controller',
            controllerAs: 'vm',
            resolve: {
                ${5:resolve}: ${5:resolve}
            }
        });
}

function ${5:resolve}() {
  ${6:innerFunction}
}
```

### ngstate
```javascript
'use strict';

angular
  .module('${1:module}')
  .config(config);

function config($stateProvider) {
  $stateProvider
    .state('${2:state}', {
      url: '/${3:url}',
      abstract: true,
      controller: '${4:controller}Controller as vm',
      templateUrl: '${5:templatUrl}',
      resolve: {
        ${6:resolve}: ${6:resolve},
      },
    })
}

function ${6:resolve}() {
  ${7:innerFunction}
}
```

### ngconfig
```javascript
'use strict';

angular
  .module('${1:module}')
  .config(${2:configName});

function ${2:configName}(${3:dependencies}) {
  ${4:innerFunction}
}
```

### ngrun
```javascript
'use strict';

angular
  .module('${1:module}')
  .run(${2:runName});

function ${2:runName}(${3:dependencies}) {
  ${4:innerFunction}
}
```

## Testing Snippets
Jon Papa recommends using Jasmine and Karma for testing. Beyond that, these tests do not have further relation to Jon Papa, they are just a styling guide we have used.

Feel free to alter this to your own style!

### ngcontrollerspec
```javascript
'use strict';

describe('${6:base description}, ', function() {
  var ${2:service}, ${1:controller}Controller, ${3:mock}Json;

  ${3:mock}Json = angular.copy(window.__fixtures__['/json/${3:mock}']);

  function ${2:service}Mock() {
    ${2:service} = jasmine.createSpyObj('${2:service}', ['${4:mockFunction}']);
    ${2:service}.${4:mockFunction}.and.returnValue(${3:mock}Json);
    return ${2:service};
  }

  beforeEach(module('${5:module}'));

  beforeEach(inject(function($controller) {
    ${1:controller}Controller = $controller('${1:controller}Controller', {
      ${2:service}: ${2:service}Mock()
    });
  }));

  describe('${7:second description}, ', function() {
    it('${8:testcase}', function() {
      expect(${2:service}.${4:mockFunction}).toHaveBeenCalled();
    });
  });
});
```

### ngservicespec
```javascript
'use strict';

describe('${7:baseDescription} ', function() {

  var ${1:service}, $q, $rootScope, ${2:mockService}, ${4:mock}Json;

  beforeEach(module('${5:module}'));

  beforeEach(function() {
    module(function($provide) {
      ${4:mock}Json = angular.copy(window.__fixtures__['/json/${4:mock}']);

      ${2:mockService} = jasmine.createSpyObj('${2:mockService}', [
        '${3:mockFunction}'
      ]);

      ${2:mockService}.${3:mockFunction}.and.returnValue(${4:mock}Json);

      $provide.value('${2:mockService}', ${2:mockService});
    });
  });

  beforeEach(inject(function(_${1:service}_, _$q_, _$rootScope_) {
    ${1:service} = _${1:service}_;
    $q = _$q_;
    $rootScope = _$rootScope_;
  }));

  describe('${8:secondDescription}', function() {
    it('${9:testCase}', function() {
      ${1:service}.${6:serviceFunction}();
      expect(${2:mockService}.${3:mockFunction}).toHaveBeenCalled();
    });
  });
})
```

### ngdescribe
```javascript
describe('${1:description}, ', function() {
  beforeEach(function() {
    ${4:beforeEach}
  });

  it('${2:testcase}', function() {
    expect(${3:value}).toBe(true);
  });
});
```

##Differences from jmiazga snippets
This snippets package is based off the execellent [angular styleguide snippets](https://github.com/jmiazga/angularjs-styleguide-snippets). This repo contains stripped down snippets, with:

* Removing the closure around each snippet, since gulp, or some other system, often handles that. If not, it is recommended you add these.
* Removed the inject service, this is recommended by jon papa, but I've moved to using a build system to handle this.
* Removed controller from Directive, prefer in a seperate file.
* Added angular.extend to top of controllers, for the members up top rule.
* New Snippets Added.

![Built For Atom](https://f.cloud.github.com/assets/69169/2290250/c35d867a-a017-11e3-86be-cd7c5bf3ff9b.gif)
