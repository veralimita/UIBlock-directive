# UIBlock-directive
Set value of yourObject.loading to true to set block busy 

## JS
```javascript
(function () {
    var app = angular.module('app');
   app.directive('blockUi', ['$document', '$interval', function ($document, $interval) {
        return {
            scope: {
                item: '='
            },
            link: function (scope, element) {
                scope.item.loading = !!scope.item.loading;

                scope.$watch('item.loading', function (to, from) {
                
                    if (!to) {
                        element.css({
                            position: 'relative',
                            cursor: 'inherit'
                        });

                        $(element).find(".busy-ui").remove()
                    }
                    else {
                        element.css({
                            position: 'relative',
                            cursor: 'wait'
                        });
                        element.append('<div class="busy-ui" style="z-index:' + element.zIndex() + 1 + '"><div class="spin-wrap"><div class="spin-center"><div class="spin"></div></div></div></div>')
                    }
                }, true);
            }
        };
    }]);
})();
```

## HTML
```html
<div block-ui item="object">
               ...
</div>
```

## CSS
```css
.busy-ui {
  position: absolute;
  top: 0;
  height: 100%;
  left: 0;
  width: 100%;
  background-color: rgba(111, 111, 111, 0.3);
}
.busy-ui .spin-wrap {
  display: table;
  width: 100%;
  height: 100%;
}
.busy-ui .spin-wrap .spin-center {
  display: table-cell;
  vertical-align: middle;
}
.busy-ui .spin-wrap .spin-center .spin {
  margin-left: auto;
  margin-right: auto;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  border: 4px dotted #faa500;
  -webkit-animation: spin 5s;
  -webkit-animation-iteration-count: infinite;
  -moz-animation: spin 5s linear infinite;
  animation: spin 5s linear infinite;
}
@-moz-keyframes spin {
  100% {
    -moz-transform: rotate(360deg);
  }
}
@-webkit-keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
  }
}
@keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
```
