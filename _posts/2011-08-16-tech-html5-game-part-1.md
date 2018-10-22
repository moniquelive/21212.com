---
id: 549
title: 'TECH: HTML5 Game &#8211; Part 1'
date: 2011-08-16T11:37:58-03:00
author: "21212"
layout: post
guid: http://local.21212.com/?p=549
permalink: /blog/tech-html5-game-part-1/
transposh_can_translate:
  - 'true'
categories:
  - Blog
---
<p style="text-align: center">
  <img class="aligncenter size-full wp-image-569" src="{{ site.url }}/assets/wp-content/uploads/2011/08/buzios.jpg" alt="" width="540" height="260" srcset="{{ site.url }}/assets/wp-content/uploads/2011/08/buzios.jpg 540w, {{ site.url }}/assets/wp-content/uploads/2011/08/buzios-300x144.jpg 300w" sizes="(max-width: 540px) 100vw, 540px" />
</p>

_&#8211; This is first post from a series of two post about how to make a HTML5 game. &#8211;_

Hello everybody! I’m here to tell you about an interesting story that happened with us.

Seven days ago, in a lunch table, the <a href="http://local.21212.com/team/" target="_blank">21 212 team</a> was talking about the features that we can use  in game development for mobile web apps. After a little discussion a goal was assigned to us: Develop an html5 cross-device game (mobile, tablet and PC) in 7 days! We thought that it’d be possible and we accepted the goal. So we started our new journey to try to acquire new knowledge and prepare us to in future to do similar things faster and help our entrepreneurs!

The game chosen for our challenge was a <a href="http://pt.wikipedia.org/wiki/Jogo_de_b%C3%BAzios" target="_blank">búzios</a> game that has simple logic and we can try using some interesting features like shake the búzios’ seashell when we are shaking a mobile with an accelerometer. In a nutshell the búzios is an afro-brazilian religion game that the guesser tries to figure out what message the divinities, called <a href="http://pt.wikipedia.org/wiki/Orix%C3%A1" target="_blank">orixás</a>, will tell the user when he throws búzios’ seashell on the basket! You need to have faith! :)

_Well&#8230; Now that we have a goal and know a lot about the búzios game it’s showtime!_

<!--more ..wanna know more about it? Go ahead!-->

To create this game we have two different challenges:

**1)** **The design challenge** &#8211; how to create a code that is compatible with different device browsers and dimensions (cross-device and cross-browser) and how to create the buzios mix animation.  We guess that we can solve both problems using CSS3 and we&#8217;ll talk about this in this post;

**2)** **The development challenge** &#8211; how to get the “devicemotion” events (accelerometer) to detect the mobile shake in web app and how to make this web app playable off-line (using cache) and how to use the audio tag. We guess that we can solve this using the html5 APIs and with a little bit of javascirpt. We&#8217;ll talk about this in next post.

Ok let’s start with the design challenge. First of all we need to create a wireframe game for better game visualization (see below picture). We used <a href="http://balsamiq.com/" target="_blank">balsamiq.com</a> to create it. Balsamiq is a good free web app tool to create wireframes!

<img class="aligncenter size-full wp-image-572" src="{{ site.url }}/assets/wp-content/uploads/2011/08/wireframe.jpg" alt="" width="540" height="254" srcset="{{ site.url }}/assets/wp-content/uploads/2011/08/wireframe.jpg 540w, {{ site.url }}/assets/wp-content/uploads/2011/08/wireframe-300x141.jpg 300w" sizes="(max-width: 540px) 100vw, 540px" />

For mobiles the basic game gui is the basket with 16 seashells, one button to mix the seashells if the device or browser doesn’t support “devicemotion events”, another button to show the result in a pop-up div, one button to turn the sound on/off, another button to show the game’s about dialog and finally an AdMob banner, so we can earn some money with ads!!! :) Now we can create the html structure that will be the same for all devices and browsers. We had some problems here because we put some images in html code, which it’s not good! We don’t have to put images or CSS style in the html structure. Here we need to have just html tags! (see code <a href="http://www.guruweb.com.br/dev/lab/buzios/html.txt" target="_blank">here</a>)

For each device we need to create its own CSS file. A good example is the <a href="http://www.guruweb.com.br/games/buzios/css/buzios-iframe.css" target="_blank">web css file</a> and the <a href="http://www.guruweb.com.br/games/buzios/css/buzios-phone.css" target="_blank">mobile css file</a> where you can see how the same html file can change completely by a CSS style. This “magic” is possible because in the html head we declarred some media queries (see below).

> <!&#8211; smartphone &#8211;>

> <link rel=&#8221;stylesheet&#8221; href=&#8221;css/buzios-phone.css&#8221; media=&#8221;only screen and (max-device-width : 480px)&#8221;>
>
> <!&#8211; ipad &#8211;>

> <link rel=&#8221;stylesheet&#8221; href=&#8221;css/buzios-ipad.css&#8221; media=&#8221;only screen and (min-width : 768px)&#8221;>
>
> <!&#8211; social networks &#8211;>

> <link rel=&#8221;stylesheet&#8221; href=&#8221;css/buzios-social-networks.css&#8221; media=&#8221;only screen and (min-width : 740px) and (max-width : 765px)&#8221;>
>
> <!&#8211; widescreen &#8211;>

> <link rel=&#8221;stylesheet&#8221; href=&#8221;css/buzios-iframe.css&#8221; media=&#8221;only screen and (min-width : 941px)&#8221;>

If you enter in the <a href="http://www.guruweb.com.br/games/buzios/" target="_blank">búzios game</a> and resize the browser window you can see in real-time the magic of CSS happening!!!! It’s amazing!!! Now we can create portable web app for PC, tablets and mobiles! You can see another example <a href="http://mediaqueri.es/popular/" target="_blank">here</a>.

The next design challenge was make an animation that shows the búzios’ mix to the user before showing the búzios’ result (which seashells are open and which seashells are closed). We thought about a lot of possible solutions: (i) create an animated gif;  (ii) create a flash animation and afterwards converting it to <a href="http://en.wikipedia.org/wiki/Scalable_Vector_Graphics" target="_blank">svg</a> by <a href="http://labs.adobe.com/technologies/wallaby/" target="_blank">Wallaby</a>: It’s a possible solution if you have a complex animation and need a tool like Flash CS5 because there isn’t a good tool to make complex cross-browser animations for CSS3, but for a simple animation it’s not the best option; (iii) make an animation writing CSS3 code: This was the best solution for us because our animation was very simple! We created some keyframes (for webkit and moz &#8211; see code below), and we added a new CSS class with animation attributes that will be added in each seashell div to play the animation.

> **CSS3 animation’s keyframes:**
>
> @-webkit-keyframes, @-moz-keyframes ANIMATE1 {

> 0% {top: 50%;}

> 40% { top: 50%; left: 90px;}

> 70% { top: 25px; left: 90px;}

> 80% { top: 312px;}

> 100% { top: 42px;}

> }
>
> **CSS class for animation:**
>
> .animate1 {

> -webkit-animation-name: ANIMATE1;

> -webkit-animation-duration: 0.25s;

> -webkit-animation-iteration-count: 1;

> -webkit-animation-timing-function: ease-in;
>
> -moz-animation-name: ANIMATE1;

> -moz-animation-duration: 0.25s;

> -moz-animation-iteration-count: 1;

> -moz-animation-timing-function: ease-in;

> }

That&#8217;s all for today! See you in the **next post**!