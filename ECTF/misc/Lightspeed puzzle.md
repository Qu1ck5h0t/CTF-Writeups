## This took me longer than I'd like to admit, but it taught me a valuable lesson in CTF - Work smarter not harder

When I opened the page, I was presented with a 10x10 scrambled grid of what appears to be parts of an image with a code on it. 

![image](https://github.com/user-attachments/assets/1682b8d0-6c5a-45d1-b23d-c9227096922c)


My first instinct was to go into the source to see what the structure looked like. I noticed that the images were conveniently named "/static/x_y.png", so I knew I could sort it by rearranging the images. 
At first I tried a manual approach, which wasn't very bright because it exceeded the 20 second time allocation I was given by about 8 minutes. When I reloaded the page, the code was a different one so i wasn't able to reuse the result either.

![image](https://github.com/user-attachments/assets/a1fc0206-5631-4e6f-b20c-b972f0156644)


So then I realised that my only option was to automate it, and with the naming format in mind, I made a tampermonkey script that sorts the images based on their x_y values.
```javascript
(function() {
    'use strict';

    // Select all relevant images
    const images = Array.from(document.querySelectorAll('img[src^="/static/"]'))
        .filter(img => img.src.match(/\d+_\d+\.png$/));

    if (images.length === 0) return;

    // Get parent container
    const container = images[0].parentNode;

    // Sort images numerically
    images.sort((a, b) => {
        const getCoords = src => {
            const [x, y] = src.match(/(\d+)_(\d+)\.png$/).slice(1,3).map(Number);
            return x * 10 + y; // Combine coordinates for sorting
        };
        return getCoords(a.src) - getCoords(b.src);
    });

    // Reinsert sorted images
    images.forEach(img => img.remove()); // Remove from current positions
    images.forEach(img => container.appendChild(img)); // Add back in order
})();
```


When I reloaded the page, the puzzle solved quicker than the speed at which the images loaded, and I was able to enter the code.

![image](https://github.com/user-attachments/assets/f1e3df01-8eea-4094-9e04-2cf13b1d661f)

![image](https://github.com/user-attachments/assets/0a7231a9-d6d9-4cd6-bb6c-4acf15acc027)
```
ECTF{Autom4t3d_PuZz13}
```
