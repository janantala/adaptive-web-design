# adaptive-speech v0.3.0 [![Build Status](https://travis-ci.org/angular-adaptive/adaptive-speech.png?branch=master)](https://travis-ci.org/angular-adaptive/adaptive-speech)

This module allows you to control web app using voice commands. It's based on Chrome's speech recognition API.

### Demo

Check out http://angular-adaptive.github.io/adaptive-speech/demo/

### References

We recomend you to read:
- [A More Awesome Web](http://moreawesomeweb.com) presentation from Google IO 2013 by Eric Bidelman
- [Voice Driven Web Apps](http://updates.html5rocks.com/2013/01/Voice-Driven-Web-Apps-Introduction-to-the-Web-Speech-API) article from HTML5 ROCKS by Glen Shires

# Requirements

- AngularJS v ~1.2.x

# Usage

We use [bower](http://twitter.github.com/bower/) for dependency management. Add

```json
dependencies: {
    "angular-adaptive-speech": "latest"
}
```

To your `bower.json` file. Then run

    bower install

This will copy the speech recognition files into your `bower_components` folder, along with its dependencies. Load the script files in your application:

```html
<script type="text/javascript" src="bower_components/angular/angular.js"></script>
<script type="text/javascript" 
    src="bower_components/angular-adaptive-speech/angular-adaptive-speech.min.js">
</script>
```

Add the adaptive.speech module as a dependency to your application module:

```js
var myAppModule = angular.module('MyApp', ['adaptive.speech']);
```

and include $speechRecognition, $speechSynthetis, $speechCorrection service as a dependency to your controller:

```js
angular.module('MyApp').controller('MainCtrl', 
    function ['$scope', '$speechRecognition, $speechSynthetis', 
    ($scope, $speechRecognition, $speechSynthetis) {

}]);
```

To start speech recognition run from controller:

```js
$speechRecognition.onstart(function(){
  $speechSynthetis.speak('Yes? How can I help you?', 'en-UK');
});
$speechRecognition.setLang('en-UK'); // Default value is en-US
$speechRecognition.listen();
```

Apply the directive to your elements where *reference* is keyword reference:

```html
<ul>
    <li 
      ng-repeat="todo in todos | filter:statusFilter track by $index"
      speechrecognition="{'tasks': recognition['en-US']['listTasks'], 'reference': todo}">
        {{todo}}
    </li>
</ul>
```
Or run recognition directly from controller:

```js
$speechRecognition.listenUtterance($scope.recognition['en-US']['addToList']);
```

## Options

All the speechRecognition options can be set up in your controller.

```js
myAppModule.controller('MyController', function($scope) {
    $scope.recognition = {};
    $scope.recognition['en-US'] = {
        'addToList': {
            'regex': /^to do .+/gi,
            'lang': 'en-US',
            'call': function(e){
                $scope.addToList(e);
            }
        },
        'listTasks': [{
            'regex': /^complete .+/gi,
            'lang': 'en-US',
            'call': function(e){
                $scope.completeTask(e);
            }
        },{
            'regex': /^remove .+/gi,
            'lang': 'en-US',
            'call': function(e){
                $scope.removeTask(e);
            }
        }]
    };
});
```

# API

## $speechRecognition

### onstart(fn)
On start event.
```js
$speechRecognition.onstart(function(e){
    // onstart
});
```

### onerror(fn)
On error event.
```js
$speechRecognition.error(function(e){
    // onerror
});
```

### onUtterance(cb)
On recognised utterance callback.
```js
$speechRecognition.onUtterance(function(utterance){
    console.log(utterance); // buy a milk
});
```

### setLang(lang)
Set recognition language.
```js
$speechRecognition.setLang('en-US');
```

To change language when recognition is already running you need to also restart recognizer:
```js
$speechRecognition.stopListening();
$speechRecognition.listen();
```

### getLang()
Get recognition language.
```js
$speechRecognition.getLang(); // 'en-US'
```
### payAttention()
Continue speech recognition after pause caused by `ignore()`. You don't need user permision again.

```js
$speechRecognition.payAttention();
```

### ignore()
Pause speech recognition.
```js
$speechRecognition.ignore();
```

### listen()
Start speech recognition. User permission is required.
```js
$speechRecognition.listen();
```

### stopListening()
Stop speech recognition.
```js
$speechRecognition.stopListening();
```

### command(utterance)
Call uterance manually.
```js
$speechRecognition.command('do something');
```

### listenUtterance(tasks)
Add listener for task
```js
var task = {
    'regex': /^do .+/gi,
    'lang': 'en-US',
    'call': function(utterance){
      // do something with utterance 'do something'
    }
};
$speechRecognition.listenUtterance(task);
```

## $speechSynthetis

### speak(text, lang)
Speak utterance.

```js
$speechSynthetis.speak('Hello there!', 'en-US');
```
### justSpoke()
Return true after `speak()` has been called.
```js
$speechSynthetis.justSpoke(); // true or false
```

### recognised()
Manualy mark speechSynthetis voice as recognised. justSpoke will be `true`.
```js
$speechSynthetis.recognised();
```

## $speechCorrection
Correct speech recognition. After incorrect recognition utterance will be corrected.

### addUtterance(utterance, correction, lang)
Create a key - value pair with incorret recognition, correction and language.
```js
$speechCorrection.addUtterance('to something', 'do something', 'en-US');
```

### removeUtterance(utterance, lang)
Remove utterance correction.
```js
$speechCorrection.removeUtterance('to something', 'en-US');
```

### addLangMap(lang, map)
Add complete correction map for a language.
```js
var map = {
    'to something': 'do something',
    'pseudo make me a sandwich': 'sudo make me a sandwich'
};
$speechCorrection.addUtterance('en-US', map);
```

### clearLangMap(lang)
Remove language map.
```js
$speechCorrection.clearLangMap('en-US');
```

### getCorrectionMap()
Get correction map for all languages.
```js
$speechCorrection.getCorrectionMap();
//  {
//      'en-US: {
//          'to something': 'do something',
//          'pseudo make me a sandwich': 'sudo make me a sandwich'
//      }
//  }
```

### getLangMap(lang)
Get correction map for a language.
```js
$speechCorrection.getCorrectionMap('en-US');
//  {
//      'to something': 'do something',
//      'pseudo make me a sandwich': 'sudo make me a sandwich'
//  }
```

### getCorrection(utterance, lang)
Get a single utterance correction.
```js
$speechCorrection.getCorrection('pseudo make me a sandwich', 'en-US'); 
// 'sudo make me a sandwich'
```

## speechrecognition directive
Add listener to html element.
- tasks: configuration object (*remove something*)
- reference: element reference name (*something*)

```html
<li
  ng-repeat="todo in todos | filter:statusFilter track by $index"
  speechrecognition="{'tasks': recognition['en-US']['listTasks'], 'reference': todo}">
    {{todo}}
</li>
```

# Testing

We use karma and jshint to ensure the quality of the code. The easiest way to run these checks is to use grunt:

    npm install -g grunt-cli
    npm install
    bower install
    grunt

The karma task will try to open Chrome as a browser in which to run the tests. Make sure this is available or change the configuration in `test/test.config.js` 

# Contributing

Pull requests are welcome. 

Make a PR against canary branch and don't bump any versions. 

Please respect the code style in place.