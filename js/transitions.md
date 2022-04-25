# transitions

#js

[https://github.com/baianat/leaps](https://github.com/baianat/leaps)

[https://habr.com/ru/post/497456/](https://habr.com/ru/post/497456/)

[https://stackoverflow.com/questions/11679567/using-css-for-a-fade-in-effect-on-page-load](https://stackoverflow.com/questions/11679567/using-css-for-a-fade-in-effect-on-page-load)

barba working code + data-barba="container" data-barba-namespace="page-a" на секции

```js
<!-- load barba (UMD version) -->
      <script src="https://unpkg.com/@barba/core"></script>

      <!-- load gsap animation library (minified version) -->
      <script src="https://unpkg.com/gsap@latest/dist/gsap.min.js"></script>

      <!-- init barba with a simple opacity transition -->
      <script type="text/javascript">
        barba.init({
transitions: [
{
name: 'opacity-transition',
leave(data) {
window.scrollTo(0, 0)
gsap.to(data.current.container, {opacity: 0});
},
enter(data) {
window.scrollTo(0, 0)
gsap.from(data.next.container, {opacity: 0});
}
}
]
});
      </script>
```