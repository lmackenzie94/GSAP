# GSAP Reference

### Random Code Examples:

[**EXAMPLE ONE**](https://www.youtube.com/watch?v=5RyrIPCs47A)
- uses: TimelineLite, CSSPlugin, TweenLite

```javascript
const navButton = document.querySelector(".nav-button");
const navOpen = document.querySelector(".nav-open");

const tl = new TimelineLite({ paused: true, reversed: true }); // start paused and reversed. Nav buttons are used to kick it off/toggle it
// NOTE: 'reverse: true' fixed an issue of having the click the play button twice for the animation to work

tl.to('.cover', 1, {
  width: '60%',
  ease: Power2.easeOut,
})
  .to('nav', 1, { height: '100%' }, '-=0.5')
  // fromTo allows us to define what values to animate from
  .fromTo('.nav-open', 0.5,
  // from
   {
      opacity: 0, 
      x: 50,
  }, 
  // to
  {
    opacity: 1,
    x: 0,
    // do something when animation completes:
    onComplete: function() {
        navOpen.style.pointerEvents = 'auto'
        console.log('DONE!')
    }
  });

  navButton.addEventListener('click', (e) => {
      // if the animation is currently running, don't allow a click to stop the animation 
      // i.e. can't click fast to play/stop the animation, must wait for it to fully finish
      if (tl.isActive()) {
        e.preventDefault();
        e.stopImmediatePropagation();
        return false
      }
      toggleTween(tl)
  } )

  function toggleTween(tween){
      tween.reversed() ? tween.play() : tween.reverse();
  }
```
