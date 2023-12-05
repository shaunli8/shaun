---
toc: false
comments: false
layout: post
title: Mario on Platform
description: Early steps in adding Mario into OOP Game. This also includes a level change.
type: plans
courses: {compsci: {week: 0} }
categories: [C1.4]
---

<!-- Liquid code, run by Jekyll, used to define location of asset(s) -->
{% assign backgroundFile = site.baseurl | append: page.images.background.src %}
{% assign platformFile = site.baseurl | append: page.images.platform.src %}
{% assign backgroundFileAlt = site.baseurl | append: page.images.backgroundAlt.src %}
{% assign backgroundFileCastles = site.baseurl | append: page.images.backgroundCastles.src %}
{% assign backgroundFileGameOver = site.baseurl | append: page.images.backgroundGameOver.src %}

{% assign playerFile = site.baseurl | append: page.images.mario.src %}

<style>
    #controls {
        position: relative;
        z-index: 2; /*Ensure the controls are on top*/
    }
</style>

<!-- Prepare DOM elements -->
<!-- Wrap both the canvas and controls in a container div -->
<div id="canvasContainer">
    <div id="controls"> <!-- Controls -->
        <!-- Background controls -->
        <button id="toggleCanvasEffect">Invert</button>
    </div>
</div>


<script type="module">
    import GameEnv from '{{site.baseurl}}/assets/js/mario/GameEnv.js';
    import GameLevel from '{{site.baseurl}}/assets/js/mario/GameLevel.js';
    import GameManager from '{{site.baseurl}}/assets/js/mario/GameManager.js';

    // Setup Globals
    GameEnv.gameSpeed = 2;
    GameEnv.gravity = 3;

    // Level One completion
    function testerCompletion() {
        console.log(GameEnv.player?.x)
        if (GameEnv.player?.x > 500) {
            return true;
        } else {
            return false;
        }
    }

    // Initalize different levels to game
    var levels = [ new GameLevel(), new GameLevel(), new GameLevel(), new GameLevel() ];
    // mario hills
    levels[0].setBackgroundFile('{{backgroundFile}}');
    levels[0].setPlatformFile(`{{platformFile}}`);
    levels[0].setPlayerFile(`{{playerFile}}`);
    levels[0].setNextLevel(levels[1]);
    levels[0].setIsComplete(testerCompletion);
    // alien planet
    levels[1].setBackgroundFile('{{backgroundFileAlt}}');
    levels[1].setPlatformFile(`{{platformFile}}`);
    levels[1].setPlayerFile(`{{playerFile}}`);
    levels[1].setNextLevel(levels[2]);
    levels[1].setIsComplete(testerCompletion);
    // castles, no platform
    levels[2].setBackgroundFile('{{backgroundFileCastles}}');
    //levels[2].setPlatformFile(`{{platformFile}}`);
    levels[2].setPlayerFile(`{{playerFile}}`);
    levels[2].setNextLevel(levels[3]);
    levels[2].setIsComplete(testerCompletion);
    // mario hills, no player
    levels[3].setBackgroundFile('{{backgroundFileGameOver}}');

    // create listeners
    toggleCanvasEffect.addEventListener('click', GameEnv.toggleInvert);
    window.addEventListener('resize', GameEnv.resize);

    // start game
    await GameManager.startGame( levels[0] );

</script>
