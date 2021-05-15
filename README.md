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

## CSS Animations

There are two ways to add animations in CSS, either through __transitions__ or __animations__. 

Phases Vue go through to add elements onto the page - Vue divides the animations into frames. 

Vue takes care of adding the classes, not the animation itself.

### A set of classes can be added for animation when adding the element to the document. 

- The __before-enter__ hook is triggered before the animetion starts. 
    - Prepare and set initial properties. 
- The __enter__ hook is where the animation performs. 
    - This is where most of the code will be written
- The __after-enter__ hook is called when the animation is complete. 
    - Allows clean-up to be done when necessary. 

- The __before-leave__ hook is triggered before the animation starts. 
- The __leave__ hook is where the animation performs. 
- The __after-leave__ hook is called when the animation is complete. 



### The Entering clases are added when the element is being inserted into the DOM. 
- The __*-enter-from__ is added to the first frame of the animation. 
    - Prepare and set initial properties. 
- The __*-enter-to__ is added to the final frame of the animation. 
    - Not commonly used, but useful if you want to add some finishing touches to the element after the animation is finished. 
- The __*-enter-active__ is added from the beginning to the end of the animation. 

Once the animation is finished, the element is added to the document. 

### The Leaving clases are added when the element is being inserted into the DOM. 

- The __*-leave-from__ is the class that gets added to the __first__ frame of the animation. 

- The __*-leave-to__ is the class that gets added to the __final__ frame of the animation. 

- The __*-leave-active__ is the class that gets added to the entire animation, including the __first__ and __final__ frames.

Once the animation is finished, the element is removed from the document. 

## Animating with CSS Transitions

### A simple way to create animation with CSS.

## Fine-tuning Transitions

### Learn how to configure transitions. There are various things that can be changed to get the desired behavior. 

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

### Animation can be applied to elements using the __v-show__ directive as well. 

```
<transition name="fade" duration="1000">
  <h2 v-show="flag">Hello World!</h2>
</transition>
```

The above would work as well.

#### v-if & v-else
Transition animation is not limited to one root element. By using __v-else__, can apply the animation as well. 

However, we do need to add a __key__ attribute as Vue will have a problem differentiating between 2 elements even though there's a conditional directive applied to them. 

__By the way, make sure to keep the transition section clean.__
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

## Animating with CSS Animations

A more advanced way to create animations, gives you more control over your animations. 

The same set of classes can be used. It can also be used along with Transition. However, if the two animation have different duration times, by defualt, __Vue will use the duration with the longest time__. But Vue does allow you to choose which duration to use. 

```
<!-- the type will either be 'animation' or 'transition' to tell Vue which duration to use -->

<transition name="zoom" type="animation">
    <h2 v-if="flag">Hello!</h2>
</transition>
```

### Playing Animation On Page Load

Does not happen by default. In order to have animation play on page load, a property __appear__ can be added to the __transition__ component. 

```
<transition name="zoom" type="animation" appear>
    <h2 v-if="flag">Hello!</h2>
</transition>
```

<hr />

## JavaScirpt Animations

CSS is usually the way to go when animating elements. It is the __Simplest__ way of adding animations. You can also animate your elements with JavaScript if you need more __control__. 

Vue provides 3 hooks to use for both __entering__ and __leaving__ animations. 

### The Entering animations are used when the element is being inserted into the DOM. 
- The __before-enter__ hook is triggered before the animetion starts. 
    - Prepare and set initial properties. 
- The __enter__ hook is where the animation performs. 
    - This is where most of the code will be written
- The __after-enter__ hook is called when the animation is complete. 
    - Allows clean-up to be done when necessary. 

### The __Leaving__ animations are used when the element is being removed from the DOM. 
- The __before-leave__ hook is triggered before the animation starts. 
- The __leave__ hook is where the animation performs. 
- The __after-leave__ hook is called when the animation is complete. 

### JavaScript animations can be added by adding __event listeners__ to the transition component. 

```
<transition
@before-enter=""
@enter=""
@after-enter=""
@before-leave=""
@leave=""
@after-leave=""
>
...
</transition>
```

There are two other events that can be listened for, which are the __cancel__ event. These events are cancelled whenever their respective animations are cancelled. 

Not often used, but available. 

```
@enter-cancelled
@leave-cancelled
```

Both __enter__ and __leave__ functions __MUST__ accept the __done__ argument. The __done__ argument are being passed in as a _function_. 

The __done__ function is a callback function that tells Vue when the animation is finished playing. 

```
leave(el, done) {
    console.log('leave event fired', el);

    const animation = el.animate([{}, { transform: "scale3d(0,0,0)" }], {
     duration: 1000,
    }); // only exist on DOM object
      
    animation.onfinish = () => done();
}
```

After the function is called, Vue will proceed with adding or removing the element. 

### Web Animations API

Not related to Vue, but can be used to perform animations using JavaScript efficiently. 

The animate() function only exists on DOM objects, and therefore it is not specific to Vue. 

Vue prefers CSS animations to be used over JavaScript animation, and therefore will check if there is a CSS animation for the transition first. This takes more resources, and to avoid, we should tell Vue we don't have a CSS animation if there doesn't exist one. 

```
<transition :css="false">
...
</transition>
```

We can bind a property called __css__ to tell Vue we don't have a CSS animation.

## Using CSS and JavaScript Transitions

When both CSS and JavaScript animations are used, Vue will use the duration set for CSS. And therefore, the done() function becomes optional for JavaScript hooks. 

<hr />

## Animating a List

So far, we been only animating a single element, or a group of elements using the conditional directive. What if we want to animate a list? 

The __transition__ component CANNOT be used to animate a list. It only works on single elements. 

A different component must be used to animate a list of elements. 

__transition-group__ is used to animate group of elements in a loop. It is similar to the __transition__ component, except it cannot set the __mode__ property. It can't be set to out-in or in-out. 

### How to Handle Sibling Animation

Vue will add a class __*-move__ to the elements being moved over. 

However, this does not solve the problem entirely. 

When an element is added, it first takes up a space, add the element and then plays the animation. When removing an element, the opposite happens, the animation gets played first before the element is removed. The other elements technically doesn't have to move in this case, and the transform property does not change. 

Solution: Use __absolute__ positioning.