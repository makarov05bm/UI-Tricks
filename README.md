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
