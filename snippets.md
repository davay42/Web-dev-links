# snippets

- **Add CSS via JS ****
    
    if you want to add css text
    
    ```js
    var style = document.createElement('style');
    style.type = 'text/css';
    style.innerHTML = 'content';
    document.getElementsByTagName('head')[0].appendChild(style);
    ```
    
    if you want to add css file
    
    ```js
    var link = document.createElement('link');
    link.setAttribute('rel', 'stylesheet');
    link.setAttribute('type', 'text/css');
    link.setAttribute('href', 'css/my.css');
    document.getElementsByTagName('head')[0].appendChild(link);
    ```
    
    [https://stackoverflow.com/questions/4847313/dynamically-add-css-to-page-via-javascript](https://stackoverflow.com/questions/4847313/dynamically-add-css-to-page-via-javascript)**

- JS
  - format time
        
    ```js
    const formatDuration = ms => {
      if (ms < 0) ms = -ms;
      const time = {
        day: Math.floor(ms / 86400000),
        hour: Math.floor(ms / 3600000) % 24,
        minute: Math.floor(ms / 60000) % 60,
        second: Math.floor(ms / 1000) % 60,
        millisecond: Math.floor(ms) % 1000
      };
      return Object.entries(time)
        .filter(val => val[1] !== 0)
        .map(([key, val]) => `${val} ${key}${val !== 1 ? 's' : ''}`)
        .join(', ');
    };
    
    // Examples
    formatDuration(1001); // '1 second, 1 millisecond'
    formatDuration(34325055574); // '397 days, 6 hours, 44 minutes, 15 seconds, 574 milliseconds'
    ```
        
  - difference in days
      
    ```js
    const getDaysDiffBetweenDates = (dateInitial, dateFinal) =>
      (dateFinal - dateInitial) / (1000 * 3600 * 24);
    
    // Example
    getDaysDiffBetweenDates(new Date('2017-12-13'), new Date('2017-12-22')); // 9
    ```
        
  - [https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_tolocalestring_date_all](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_tolocalestring_date_all)
    
  - [https://habr.com/ru/company/macloud/blog/557422/](https://habr.com/ru/company/macloud/blog/557422/)