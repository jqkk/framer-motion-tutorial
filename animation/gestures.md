## Animation Helpers

- motion 컴포넌트는 여러 gesture 애니메이션 props를 제공한다.
- `whileHover`, `whileTap`, `whileFocus`, `whileDrag`, `whileInView`
- 제스처가 활성화되어 있는 동안 일시적으로 애니메이션을 적용할 애니메이션 대상을 정의할 수 있다.

## Hover

### whileHover
```jsx
<motion.div whileHover={{ scale: 1.2 }} />
```

### onHoverStart
```jsx
<motion.div onHoverStart={() => console.log('Hover starts')} />
```

### onHoverEnd
```jsx
<motion.div onHoverEnd={() => console.log("Hover ends")} />
```

## Focus

### whileFocus
```jsx
<motion.input whileFocus={{ scale: 1.2 }} />
```

## Tap

### whileTap
```jsx
<motion.div whileTap={{ scale: 0.8 }} />
```

### onTap
```jsx
function onTap(event, info) {
  console.log(info.point.x, info.point.y)
}

<motion.div onTap={onTap} />
```

### onTapStart
```jsx
function onTapStart(event, info) {
  console.log(info.point.x, info.point.y)
}

<motion.div onTapStart={onTapStart} />
```

### onTapCancel
```jsx
function onTapCancel(event, info) {
  console.log(info.point.x, info.point.y)
}

<motion.div onTapCancel={onTapCancel} />
```

## Pan

### onPan
```jsx
function onPan(event, info) {
  console.log(info.point.x, info.point.y)
}

<motion.div onPan={onPan} />
```

### onPanStart
```jsx
function onPanStart(event, info) {
  console.log(info.point.x, info.point.y)
}

<motion.div onPanStart={onPanStart} />
```

### onPanEnd
```jsx
function onPanEnd(event, info) {
  console.log(info.point.x, info.point.y)
}
```

## Drag

### whileDrag
```jsx
<motion.div whileDrag={{ scale: 1.2 }} />
```

### drag
- default는 false로 설정된다.
- true로 설정하면 x,y 축으로 드래그할 수 있다.
- 특정 방향으로만 드래그하려면 x또는 y로 지정한다.

```jsx
<motion.div drag="x" />
```

### dragConstraints
```jsx
// In pixels
<motion.div
  drag="x"
  dragConstraints={{ left: 0, right: 300 }}
/>

// As a ref to another component
const MyComponent = () => {
  const constraintsRef = useRef(null)

  return (
     <motion.div ref={constraintsRef}>
         <motion.div drag dragConstraints={constraintsRef} />
     </motion.div>
  )
}
```