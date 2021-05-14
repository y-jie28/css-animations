# animations

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

<hr />

# Notes

There are two ways to add animations in CSS, either through __transitions__ or __animations__. 

Phases Vue go through to add elements onto the page - Vue divides the animations into frames. 

Vue takes care of adding the classes, not the animation itself.


## Animating with CSS Transitions

- A set of classes can be added for when adding the element to the document. 

#### *-enter-from

__*-enter-from__ is the class that gets added to the __first__ frame of the animation. e.g. if the animation is called __fade__, it will be:  

```
fade-enter-from
```

It isn't alive for very long, its purpose is to add some initial properties to the element. 

#### *-enter-to

__*-enter-to__ is the class that gets added to the __final__ frame of the animation. 

This class isn't commonly used, but is useful if you want to add some finishing touches to the element after the animation is finished. 

#### *-enter-active

__*-enter-active__ is the class that gets added to the __beginning__ of the animation to the __end__ of the animation, which includes the __first__ and __final__ frames. 

Once the animation is finished, the element is added to the document. 

- A different set of classes can be added for leaving the document. 

__*-leave-from__ is the class that gets added to the __first__ frame of the animation. 

__*-leave-to__ is the class that gets added to the __final__ frame of the animation. 

__*-leave-active__ is the class that gets added to the entire animation, including the __first__ and __final__ frames.

Once the animation is finished, the element is removed from the document. 

## Fine-tuning Transitions

- Learn how to configure transitions. There are various things that can be changed to get the desired behavior. 


The following code didn't tell Vue how long the animation should play. Vue is capable of looking at the styles applied to the element, where the duration was set. Vue will use the duration that was set in the CSS. 

```
<template>
<transition name="fade">
    <h2 v-if="flag">Hello World!</h2>
</transition>
</template>

<styles>
.fade-enter-active {
  transition: all 0.25s linear;
}
</styles>
```

It is possible to set the duration by adding the __duration__ property on the __transition__ component. The value for the duration property must be in milliseconds. 

```
<transition name="fade" duration="1000">
  <h2 v-if="flag">Hello World!</h2>
</transition>
```

Vue will priortize duration property over the duration that was defined in the CSS on the component.

- Animation can be applied to elements using the __v-show__ directive as well. 

```
<transition name="fade" duration="1000">
  <h2 v-show="flag">Hello World!</h2>
</transition>
```

The above would work as well.

#### v-if & v-else
Transition animation is not limited to one root element. By using __v-else__, can apply the animation as well. 

However, we do need to add a __key__ attribute as Vue will have a problem differentiating between 2 elements even though there's a conditional directive applied to them. 

___By the way, make sure to keep the transition section clean. ___
(_I spent 10 minutes debugging why the conditional directive is not working and it turns out the comments caused the problem =皿=#_)

```
  <transition name="fade">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <!-- not limited to one root element -->
    <h2 v-else key="secondary">Another Hello!</h2>
  </transition>
```

The above will __NOT__ work. 

#### Animate In-and-Out
Default behavior is the second element animates in first before the first element animates out. The behavior can be reversed (first element to animate out first before second elements animates in) by using the __mode__ attribute. 

The __mode__ attribute defines the order of the animation. 

```
<!-- The default of mode is "in-out" -->
<transition mode="out-in"> 
</transition>
```




