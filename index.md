<style>

.gallery {
    display: flex;
}

.galpanel {
    position: relative;
    height: 500px;
    width: 250px;
    overflow: hidden;
    display: inline-block;
    margin-left: 0.1em;
    margin-right: 0.1em;
}

.overlay {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%;
    width: 100%;
    opacity: 25%;
    transition: .5s ease;
    background-color: #000000;
}

.text-overlay {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    height: 100%;
    width: 100%;
    opacity: 0;
    transition: .5s ease;
    background-color: none;
}

.galpanel:hover .overlay {
    opacity: 50%;
    mix-blend-mode: darken;
}

.galpanel:hover .text-overlay {
    opacity: 100%;
}

.galimage {
    display: block;
    height: 500px;
    position:absolute;
    left: -100%;
    right: -100%;
    top: -100%;
    bottom: -100%;
    margin: auto;
    width: auto;
}

.galpanel > img {
    max-width: unset;
}

.galtext {
    color: white;
    font-size: 20px;
    position: absolute;
    top: 50%;
    left: 50%;
    -webkit-transform: translate(-50%, -50%);
    -ms-transform: translate(-50%, -50%);
    transform: translate(-50%, -50%);
    text-align: center;
}

.galtext > a:link, a:visited {
    text-decoration: none;
    color: inherit;
}

.galtext > a:hover, a:active {
    text-decoration: none;
    color: inherit;
}

</style>

Welcome! This is where I'll be keeping any thoughtful bites or chews that I come across.

<div id="gallery">
<div class="galpanel">
    <img src="https://github.com/alextongue/hrtf-pca/blob/master/writeup/itd_iid.png?raw=true"
    class="galimage">
    <a href="https://alextongue.github.io/workbench/">
        <div class="overlay"></div>
    </a>
    <div class="textoverlay">
        <div class="galtext">
            <a href="https://alextongue.github.io/digest/lit/">Literature</a>
        </div>
    </div>
</div>

<div class="galpanel">
    <img src="https://github.com/alextongue/alextongue.github.io/blob/master/digest/_pics/notes_cover.png?raw=true"
    class="galimage">
    <a href="https://alextongue.github.io/workbench/">
        <div class="overlay"></div>
    </a>
    <div class="textoverlay">
        <div class="galtext">
            <a href="https://alextongue.github.io/digest/notes/">Notes</a>
        </div>
    </div>
</div>

<div class="galpanel">
    <img src="https://github.com/alextongue/alextongue.github.io/blob/master/workbench/resources/m85/dark3.jpg?raw=true"
    class="galimage">
    <a href="https://alextongue.github.io/workbench/">
        <div class="overlay"></div>
    </a>
    <div class="textoverlay">
        <div class="galtext">
            <a href="https://alextongue.github.io/workbench/">Workbench</a>
        </div>
    </div>
</div>
</div>