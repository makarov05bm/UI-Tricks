# UI-Tricks

## Smooth Dropdown
```js
    const [height, setHeight] = useState(0)

    useEffect(() => {
        mainContent.current.style.setProperty('--openHeight', mainContent.current.scrollHeight + 'px')
        setHeight(mainContent.current.style.getPropertyValue('--openHeight'))
    })

    const handleToggle = () => {
        setActive(prev => !prev)
        console.log(height);

        if (active) {
            mainContent.current.style.height = '0'
        } else {
            mainContent.current.style.height = height
        }
    }
```

```css
    .content {
        height: 0;
        transition: height 0.2s cubic-bezier(.51, .92, .24, 1.0);
        
        // the padding on a child ul or div not .content
    }
```

<br/>

## Postion Absolute At Middle Of Elements
```css
    position: absolute;
    left: 50%;
    top: 100%;
    transform: translateX(-50%); 
```

<br/>

## Blur Background
```css
.main-page {
    height: 80vh;
    display: flex;
    flex-direction: column;
    position: relative;
    border-bottom: 1px solid rgba(#2A2928, 0.5);
    
    .hero {
        flex: 1;
    }

    &::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-image: url('/images/car.jpg');
        background-size: 70%;
        background-position: center;        
        background-repeat: no-repeat;
        z-index: -1;
        filter: blur(80px);
    }
}
```

<br/>

## Triangles
```css
width: 0; 
height: 0; 
border-left: 6px solid transparent;
border-right: 6px solid transparent;
border-bottom: 6px solid rgba($plain-dark, 0.6);
```

<br/>

## Page scroll

```css
* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}

body {
    min-height: 5000px;
    background-color: #eee;
}

.scroller {
    position: fixed;
    left: 0;
    top: 0;
    width: 0;
    height: 5px;
    background-color: #0075ff;
    z-index: 1000;
}
```

```js
let el = document.querySelector('.scroller')
let height = document.documentElement.scrollHeight - document.documentElement.clientHeight

document.addEventListener('scroll', () => {
    let scrollTop = document.documentElement.scrollTop
    el.style.width = `${(scrollTop / height) * 100}%`
})
```

<br/>

## Gradient Animation

```css
body {
	background: linear-gradient(-45deg, #ee7752, #e73c7e, #23a6d5, #23d5ab);
	background-size: 400% 400%;
	animation: gradient 15s ease infinite;
	height: 100vh;
}

@keyframes gradient {
	0% {
		background-position: 0% 50%;
	}
	50% {
		background-position: 100% 50%;
	}
	100% {
		background-position: 0% 50%;
	}
}

```

<br/>

## Prevent scrolling on an element

```js
menu.addEventListener('wheel', preventScroll)

const preventScroll = (e) => {
    e.preventDefault()
    e.stopPropagation()

    return false
}
```

<br/>

## Paper squares

```css
background-size: 40px 40px;
  background-image:
    linear-gradient(to right, grey 1px, transparent 1px),
    linear-gradient(to bottom, grey 1px, transparent 1px);
```

<br/>

## hr

```css
hr {
    border: 0;
    height: 1px;
    background-image: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0));
}
```

<br/>

## Style Navbar On Scroll

```js
const [isActive, setIsActive] = useState(false)

    useEffect(() => {
        window.onscroll = () => {
            if (window.scrollY > 100) {
                setIsActive(true)
            } else {
                setIsActive(false)
            }
        }
    }, [])
```

<br/>

## Youtube Videos

```html
<iframe width="420" height="315"
	src="https://www.youtube.com/embed/1ENiVwk8idM">
</iframe>
```

<br/>

## Detect if device is a phone

```js
/Android|iPhone/i.test(navigator.userAgent)
```

<br/>

## Animation on intersaction

> The element we want to animate initially has the `className` hidden

```js
useEffect(() => {
    const observer = new IntersectionObserver((entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('show')
        } else {
          entry.target.classList.remove('show')
        }
      })
    })

    observer.observe(procedureRef.current)
  }, [])
```

```css
.hidden {
    opacity: 0;
    filter: blur(4px);
    transition: all 1.2s;
}

.show {
    opacity: 1;
    filter: blur(0);
}
```

## color-scheme

```scss
// normal: Indicates that the element isn't aware of any color schemes, and so should be rendered using the browser's default color scheme
color-scheme: normal;
color-scheme: light;
color-scheme: dark;
color-scheme: light dark;
// only: Forbids the user agent from overriding the color scheme for the element
color-scheme: only light;

// To opt the entire page into the user's color scheme preferences declare color-scheme on the :root element.

:root {
  color-scheme: light dark;
}
```

<br/>

## Number Formatter

```js
let formatter = Intl.NumberFormat('en', { notation: 'compact' });

<p>{formatter.format(nbrLikes)}</p>
```

<br/>

## Textarea auth heigh stretching

```css
.txtstuff {
    resize: none;
    overflow: hidden;
}

.hiddendiv {
    padding: 5px;
    display: block;
    white-space: pre-wrap;
    word-wrap: break-word;
    overflow-wrap: break-word;
    background-color: red;
    position: absolute;
    top: -100%;
    left: -100%;

    &::after {
        content: '\200B';
    }
}

.common {
    width: 100%;
    min-height: 80px;
    font-family: inherit;
    font-size: 0.9rem;
    overflow: hidden;
}
```

```js
    const [edit, setEdit] = useState(false)
    
    const handleInput = (e) => {
        let content = null

        if (edit) {
            content = e.target.value
            setVal(content)
            txt.current.style.height = `${hiddenDiv.current.getBoundingClientRect().height}px`
        }

        if (e.target.value === '') {
            txt.current.style.height = '20px'
        }
    }
    
    {!edit ? (
            <p className='post-body'>
                {postBody}
            </p>
        ) : (
            <>
                <textarea className='txtstuff' onChange={handleInput} ref={txt}>{postBody}</textarea>
                <div className="hiddendiv common" ref={hiddenDiv}>{val}</div>
            </>
        )}
    
```

<br/>

## Theme Switcher

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="/styles/styles.css">
    <script src="app.js" defer></script>
    <title>Document</title>
</head>
<body class="light">
    <nav class="navbar">
        <ul class="navbar-nav">
            <li class="navbar-item">Home</li>
            <li class="navbar-item">About</li>
            <li class="navbar-item">Blog</li>

            <li class="nav-item has-dropdown">
                <a href="#">Theme</a>
                <ul class="dropdown">
                    <li class="dropdown-item">
                        <a id='light' href="#">light</a>
                    </li>
                    <li class="dropdown-item">
                        <a id='dark' href="#">dark</a>
                    </li>
                    <li class="dropdown-item">
                        <a id='solar' href="#">solarize</a>
                    </li>
                </ul>
            </li>
        </ul>
    </nav>

    <header>
        <img src="logo.png" alt="logo" class="logo">
        <h1>Fron-End Web Development, <br>Fired Up</h1>

        <p>Express.js, Next.js, Javascript, mongoDB</p>
    </header>

    <main>
        Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolor iure, modi possimus illum voluptatem, reiciendis tempore rem explicabo, quo fuga corporis deleniti. Vero unde deleniti laudantium veniam excepturi nulla recusandae?
    </main>
</body>
</html>
```

```scss
:root {
    --gray0: #f8f8f8;
    --gray1: #dbe1e8;
    --gray2: #b2becd;
    --gray3: #6c7983;
    --gray4: #454e56;
    --gray5: #2a2e35;
    --gray6: #12181b;
    --blue: #0084a5;
    --purple: #a82dd1;
    --yellow: #fff565;
}

.light {
    --bg: var(--gray0);
    --bg-nav: linear-gradient(to right, var(--gray1), var(--gray3));
    --bg-dropdown: var(--gray0);
    --text: var(--gray6);
    --border-color: var(--blue);
    --bg-solar: var(--yellow);
}
  

.dark {
    --bg: var(--gray5);
    --bg-nav: linear-gradient(to right, var(--gray5), var(--gray6));
    --bg-dropdown: var(--gray6);
    --text: var(--gray0);
    --border-color: var(--purple);
    --bg-solar: var(--blue);
}

.solar {
    --gray0: #fbffd4;
    --gray1: #f7f8d0;
    --gray2: #b6f880;
    --gray3: #5ec72d;
    --gray4: #3ea565;
    --gray5: #005368;
    --gray6: #003d4c;

    --bg: var(--gray0);
    --bg-nav: linear-gradient(to right, var(--gray1), var(--gray3));
    --bg-dropdown: var(--gray0);
    --text: var(--gray6);
    --border-color: var(--blue);
    --bg-solar: var(--yellow);
}

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;   
}

body {
    line-height: 1.6;
    background: var(--bg);
    color: var(--text);
    transition: background 500ms ease-in-out, color 100ms ease-in-out;
}

ul {
    list-style-type: none;
}

a {
    color: currentColor;
    text-decoration: none;
}

.navbar {
    width: 100%;
    padding: 1rem;
    background: var(--bg-nav);
    background-color: var(--bg-nav);
}

.navbar-nav {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    height: 100%;
}

header {
    padding: 1rem;
    margin-bottom: 1rem;
    padding-bottom: 3.5rem;
    text-align: center;
    background: var(--bg-nav);
    clip-path: polygon(50% 0, 100% 0, 100% 65%, 50% 100%, 0 65%, 0 0);
}

.dropdown {
    position: absolute;
    width: 500px;
    opacity: 0;
    z-index: 2;
    border-top: 2px solid var(--border-color);
    background-color: var(--bg-dropdown);

    border-bottom-right-radius: 8px;
    border-bottom-left-radius: 8px;

    display: flex;
    align-items: center;
    justify-content: space-around;
    margin-top: 1.4rem;
    padding: 0.5rem;
    transform: translateX(-43%);

    transition: opacity 0.15s ease-out;
}

.has-dropdown:focus-within .dropdown {
    opacity: 1;
    pointer-events: auto;
}

.dropdown-item a {
    width: 100%;
    height: 100%;
    size: 0.7rem;
    padding-left: 10px;
    font-weight: bold;

    &::before {
        content: '';
        border: 2px solid #fff ;
        border-radius: 50%;
        width: 2rem;
        height: 2rem;
        display: inline-block;
        vertical-align: middle;
        margin-right: 10px;
    }
}

#dark::before {
    background: #2a2e35;
}

#light::before {
    background: #ffffff;
}

#solar::before {
    background: var(--bg-solar);
}

@keyframes color-rotate {
    from {
        filter: hue-rotate(0deg);
    } to {
        filter: hue-rotate(360deg);
    }
}

.logo:hover {
    animation-name: color-rotate;
    animation-duration: 1s;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}
```

```js
const darkBtn = document.getElementById('dark')
const lightBtn = document.getElementById('light')
const solarBtn = document.getElementById('solar')
const body = document.body

const theme = localStorage.getItem('theme')
const isSolar = localStorage.getItem('isSolar')

if (theme) {
    body.classList.add(theme)
    isSolar && body.classList.add('solar')
}

darkBtn.onclick = () => {
    body.classList.replace('light', 'dark')
    body.classList.replace('solar', 'dark')

    localStorage.setItem('theme', 'dark')
}

lightBtn.onclick = () => {
    body.classList.replace('dark', 'light')
    body.classList.replace('solar', 'light')

    lightBtn.style.cssText = `
        --gray0: #eee;
    `

    localStorage.setItem('theme', 'light')
}

solarBtn.onclick = () => {
    if (body.classList.contains('solar')) {
        body.classList.remove('solar')
        solarBtn.style.csstext = `
            --bg-solar: var(--yellow);
        `
        solarBtn.innerText = 'solarize'

        localStorage.removeItem('isSolar')
    } else {
        body.classList.replace('light', 'solar')
        body.classList.replace('dark', 'solar')
        solarBtn.innerText = 'normalize'

        localStorage.setItem('isSolar', true)
    }
}
```
