---
layout: page
title: About
permalink: /about/
---

This site is built with [fastpages](https://github.com/fastai/fastpages)

<style>
footer {
          background-color: #181818;
      } 
.timer {
  width: 200px;
  border: solid 1px #ffffff;
  border-radius: 6px;
  position: fixed;
  top: 50%;
  left: 20px;
}

.timer .inner {
  height: 15px;
  animation: timer-start;
  animation-duration: 40s;
  animation-iteration-count: 1;
  animation-fill-mode: forwards;
  animation-play-state: paused;
  animation-timing-function: linear;
  border-radius: 6px;
}

@keyframes timer-start {
  0% {
    width: 0%;
    background: #F00;
  }
  100% {
    width: 100%;
    background: #1aff00;
  }
}
</style>

## Key Links

- GitHub Repos:  <a href="https://github.com/nighthawkcoders">github.com/nighthawkcoders</a>

- AWS Deployments: <a href="https://csa.nighthawkcodingsociety.com/">csp.nighthawkcodingsociety.com</a>

- Slack: <a href="https://join.slack.com/t/cs-p-hq/shared_invite/zt-1ejp2nekj-vIeGHTAKR13E~648nh2NRg">Join Link</a>

- 2021-2022 Archives: <a href="https://padlet.com/jmortensen7/csp2022tri1">Fall</a>, <a href="https://padlet.com/jmortensen7/csp2022tri2">Early Winter</a>, <a href="https://cspcoders.nighthawkcodingsociety.com/">Late     Winter, Spring</a>


<audio id="myAudio" autoplay loop>
  <source src="{{site.baseurl}}//audios/ebyt.mp3" type="audio/mpeg">
</audio>

<div id='timer'></div>

<script>
  function initTimer(id, duration, callback) {
    var t = document.getElementById(id);
    t.className = 'timer';
    var tInner = document.createElement('div');
    tInner.className = 'inner';
    tInner.style.animationDuration = duration;
    if (typeof(callback) === 'function')
      tInner.addEventListener('animationend', callback);
      t.appendChild(tInner);

      // Check if audio is playing
      var audio = document.getElementById('myAudio');
      audio.onplay = function() {
        t.style.display = 'block';
        // Start animation
        tInner.style.animationPlayState = 'running';
      };

      audio.onpause = function() {
        t.style.display = 'none';
        // Pause animation
        tInner.style.animationPlayState = 'paused';
      };
  }

  addEventListener('load', () => {
    initTimer('timer', '228s', () => {
      // Callback function
    });
  });
</script>  
