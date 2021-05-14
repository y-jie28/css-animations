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

#### *-leave-from

__*-leave-from__ is the class that gets added to the __first__ frame of the animation. 

#### *-leave-to

__*-leave-to__ is the class that gets added to the __final__ frame of the animation. 

#### *-leave-active

__*-leave-active__ is the class that gets added to the entire animation, including the __first__ and __final__ frames.

Once the animation is finished, the element is removed from the document. 