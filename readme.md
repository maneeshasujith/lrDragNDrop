# lrDragNDrop

`lrDragNDrop` is a drag and drop module for `Angularjs` which allows to drag items from one collection and drop to another one; or reorder the items within the same collection
It is "item oriented" which imply:
  * the directives must be used with the standard ngRepeat directive
  * "adorners" can be added
  * works only with non empty collections
  * you may want to have a look at [sdfdf](sdfdsf) if you don't need this "item oriented" approach
It is about 150 lines of code and has no dependency to third party library (except the framework itself).

See demo example [here](gh-pages)

## getting started

add the module to your application using standard angularjs module management
```javascript```
angular.module('myApp',['lrDragNdrop']);

### drag source directives

add one the two following source directives to a repeated items collection to make a collection become a drag source

```markup```
<ul>
    <li ng-repeat="item in collection" lr-drag-src="anyNamespace">{{item}}</li>
</ul>

The model associated to the dragged item will be removed from the collection once it is dropped into a drop target with the same namespace (see below)

```markup```
<ul>
    <li ng-repeat="item in collection" lr-drag-src-safe="anyNamespace">{{item}}</li>
</ul>

The model associated will not be removed and a copy of the reference will be added to the target collection

Note: if you don't specify a namespace, a "global" namespace will be assumed

### drop target directive

```markup```
<ul>
    <li ng-repeat="item in targetCollection" lr-drop-target="anyNamespace">{{item}}</li>
</ul>

the targetCollection will be able to get all the dragged items if there were taken from a source with the same namespace

Note a target can be its own source (if you want to use drag and drop to reorder the items)

## adorners

when a source item is dragged over a target element and if they share the same namespace a class name is added to the target element following this rule
* ``lr-drop-target-before``, if the cursor position is above the diagonal going from the bottom left corner to the top right corner of the target element
* ``lr-drop-target-after``,if the cursor position is below the diagonal going from the bottom left corner to the top right corner of the target element

Note you can modify the source code quite easily to have something more elaborated to take the collection orientation into account

## empty collection
The directives are associated to the item elements and not on the collection container element. So if there is no element yet in the target collection you won't be able to use the drop target feature.
However you can easily attach your own directive base on the ``lrDragStore`` service to the container element to support the drop for empty target collection.

##Licence

MIT