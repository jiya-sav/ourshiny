---
layout: page
title: About
permalink: /about/
---

<html>
<head>
    <title>About Our Team</title>
    <style>
        .card-container {
            width: 300px;
            height: 400px;
            perspective: 1000px;
            margin: 20px;
            display: inline-block;
        }

        .card {
            position: relative;
            width: 75%;
            height: 100%;
            transform-style: preserve-3d;
            transition: transform 1s;
        }

        .card:hover {
            transform: rotateY(180deg);
        }

        .card-front,
        .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
        }

        .card-front {
            background-color: #000000;
            border-radius: 10px;
            padding: 20px;
            box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
        }

        .card-back {
            background-color: #000000;
            border-radius: 10px;
            padding: 20px;
            transform: rotateY(180deg);
        }

        .card img {
            width: 220px;
            height: auto;
            border-radius: 10px;
            margin-bottom: 10px;
        }

        .card h3 {
            margin-top: 0;
            font-size: 30px;
        }

        .card p {
            font-size: 28px;
        }

        .card-container:nth-child(4),
        .card-container:nth-child(5) {
            display: inline-block;
            vertical-align: top;
        }

        .second-row {
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="card-container">
        <div class="card">
            <div class="card-front">
                <img src="https://github.com/jiya-sav/ourshiny/blob/master/images/kaylee.PNG?raw=true" alt="Kaylee Hou">
                <h3>Kaylee Hou</h3>
            </div>
            <div class="card-back">
                <p>Scrum Master/Backend Developer</p>
            </div>
        </div>
    </div>
    <div class="card-container">
        <div class="card">
            <div class="card-front">
                <img src="https://github.com/jiya-sav/ourshiny/blob/master/images/sanikapic.PNG?raw=true" alt="Sanika Shahapurkar">
                <h3>Sanika Shahapurkar</h3>
            </div>
            <div class="card-back">
                <p>Devops/Backend Developer</p>
            </div>
        </div>
    </div>
    <div class="card-container">
        <div class="card">
            <div class="card-front">
                <img src="person3.jpg" alt="Trent Cardall">
                <h3>Trent Cardall</h3>
            </div>
            <div class="card-back">
                <p>Frontend Developer</p>
            </div>
        </div>
    </div>
    <div class="second-row">
        <div class="card-container">
            <div class="card">
                <div class="card-front">
                    <img src="person4.jpg" alt="Mani Taleban">
                    <h3>Mani Taleban</h3>
                </div>
                <div class="card-back">
                    <p>Frontend Developer</p>
                </div>
            </div>
        </div>
        <div class="card-container">
            <div class="card">
                <div class="card-front">
                    <img src="person5.jpg" alt="Jiya Savlani">
                    <h3>Jiya Savlani</h3>
                </div>
                <div class="card-back">
                    <p>Frontend/Backend Developer</p>
                </div>
            </div>
        </div>
    </div>
</body>
</html>


## Key Links

- GitHub Repos:  <a href="https://github.com/nighthawkcoders">github.com/nighthawkcoders</a>

- AWS Deployments: <a href="https://csa.nighthawkcodingsociety.com/">csp.nighthawkcodingsociety.com</a>

- Slack: <a href="https://join.slack.com/t/cs-p-hq/shared_invite/zt-1ejp2nekj-vIeGHTAKR13E~648nh2NRg">Join Link</a>

- 2021-2022 Archives: <a href="https://padlet.com/jmortensen7/csp2022tri1">Fall</a>, <a href="https://padlet.com/jmortensen7/csp2022tri2">Early Winter</a>, <a href="https://cspcoders.nighthawkcodingsociety.com/">Late     Winter, Spring</a>


<audio id="myAudio" autoplay loop>
  <source src="{{site.baseurl}}//audios/ebyt.mp3" type="audio/mpeg">
</audio>

