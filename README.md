# UI-Tricks

## Dropdown
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
