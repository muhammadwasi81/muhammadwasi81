### Hi there 👋 I'm Muhammad wasi

Here are some ideas to get you started:

- 🔭 I’m currently working on websites and web applications
- 🌱 I’m currently learning MERN STACK..
- 📫 How to reach me: 
email: wasiarain819@gmail.com
phone: +92 3162493262

<div class="container">
    <object data="SJLogo.svg" type="image/svg+xml" width="128" height="128" class="svg-style"></object>
    <object data="SJLogoBackdrop.svg" type="image/svg+xml" width="128" height="128" class="svg-style-prop"></object>
    <h2 class="text-backdrop">soeren.codes</h2>
</div>


.text-backdrop {
    width: 0;
    overflow: hidden;
    z-index: -1;
    position: absolute;
    animation: anim-text .45s ease-in forwards .6s;
    text-transform: uppercase;
    font-size: 2.5rem;
    font-family: 'Share Tech Mono', monospace;
}

.svg-style {
    z-index: 1;
    position: absolute;
    animation: anim-logo .45s ease-out forwards, anim-move-logo .45s ease-out forwards .55s;
}

.svg-style-prop {
    z-index: -2;
    position: absolute;
    animation: anim-boxshadow .45s ease-out forwards, anim-move-box .45s ease-out forwards .55s;
}

@keyframes anim-boxshadow {
    0% {
        transform: translate(0, 0);
    }
    100% {
        opacity: 100%;
        transform: translate(5px, 5px);
    }
}

@keyframes anim-logo {
    0% {
        transform: translate(0, 0);
    }
    100% {
        transform: translate(-5px, -5px);
    }
}

@keyframes anim-text {
    0% {
        overflow: hidden;
        transform: translateX(0);
    }
    100% {
        overflow: visible;
        transform: translateX(20px);
    }
}

@keyframes anim-move-box {
    100% {
        transform: translate(-60px, 5px);
    }
}

@keyframes anim-move-logo {
    100% {
        transform: translate(-70px, -5px);
    }
}
