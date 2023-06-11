## 간단한 애니메이션

- 대부분의 애니메이션을 `motion`컴포넌트와 animate props로 구현될 수 있다.

```jsx
<motion.div animate={{ x: 100 }} />
```

- animate props의 어떠한 value가 변경된다면, 해당 컴포넌트는 자동적으로 변경된 애니메이션을 수행한다.

## 트랜지션(Transitions)

- 기본적으로, 애니메이션 타입에 따라 적절한 트랜지션이 설정되어 있다. 예를 들어 물리적 속성(x or scale 설정)은 spring simulation으로 설정된다. 반면 opacity나 color는 tween으로 설정된다.
- transition props 설정을 통해 직접 정의내릴수 있다.

```jsx
<motion.div
  animate={{ x: 100 }}
  transition={{ ease: "easeOut", duration: 2 }}
/>
```

## 시작 애니메이션

- motion 컴포넌트가 처음 렌더되었을 때, 만일 animate 속성 값과 style 혹은 initial 값이 다르다면 자동적으로 애니메이션이 수행된다.
- initial props에 false를 주어 초기 애니메이션을 막을 수 있다.

```jsx
<motion.div animate={{ x: 100 }} initial={false} />
```

## 종료 애니메이션

- React에서 컴포넌트가 트리에서 제거되면, 컴포넌트는 즉시 제거된다.
- Framer Motion은 종료 애니메이션이 수행될 때까지 컴포넌트를 DOM에서 유지시켜주는 AnimatePresence 컴포넌트를 제공해준다.

```jsx
<AnimatePresence>
  {isVisible && (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      exit={{ opacity: 0 }}
    />
  )}
</AnimatePresence>
```

## Keyframes

- animate의 값으로 keyframes로 설정할 수 있다.(배열 형태)
- 이들은 순서대로 수행된다.

```jsx
<motion.div animate={{ x: [0, 100, 0] }} />
```

- `null` 와일드카드로 initial keyframe을 현재 엘리먼트의 스타일 값으로 설정할 수 있다.
- keyframes 애니메이션이 현재 값이라면 훨씬 더 자연스러워 보일 것이고, 코드 중복을 줄일 수 있다.

```jsx
<motion.div animate={{ x: [null, 100, 0] }} />
```

```jsx
<motion.circle cx={500} animate={{ cx: [null, 100] }} />
```

- 기본적으로 각 keyframe은 동일한 지속시간을 가진다.
- transition 속성의 times 값을 설정하여 각 keyframe의 지속시간을 설정할 수 있다.
- 0~1 사이의 값으로 정의해야한다.

```jsx
<motion.circle
  cx={500}
  animate={{ cx: [null, 100, 200] }}
  transition={{ duration: 3, times: [0, 0.2, 1] }}
/>
```

## 제스쳐

- hover, tap, drap, focus, inView와 같은 제스쳐에 대해서 애니메이션 값을 설정할 수 있다.
- 제스쳐가 종료되면 초기 값으로 돌아간다.

```jsx
<motion.button
  initial={{ opacity: 0.6 }}
  whileHover={{
    scale: 1.2,
    transition: { duration: 1 },
  }}
  whileTap={{ scale: 0.9 }}
  whileInView={{ opacity: 1 }}
/>
```

## Variants

- animate의 값으로 객체를 사용하는 것은 단순하고 간편한 컴포넌트 애니메이션에 유용하다.
- 하위 DOM으로 전파하거나, 선언적인 방법으로 애니메이션을 조율하기 위해서는 `variants` 속성을 사용할 수 있다.

```jsx
<motion.div
  initial="hidden"
  animate="visible"
  variants={{ visible: { opacity: 1 }, hidden: { opacity: 0 } }}
/>
```

## Propagation

- motion 컴포넌트에 자식 컴포넌트를 가진다면, 자식 요소가 고유의 animate 속성을 정의할 때까지 구성 요소 계층 구조를 통해 아래로 흐른다.

```jsx
const list = {
  visible: { opacity: 1 },
  hidden: { opacity: 0 },
};

const item = {
  visible: { opacity: 1, x: 0 },
  hidden: { opacity: 0, x: -100 },
};

return (
  <motion.ul initial="hidden" animate="visible" variants={list}>
    <motion.li variants={item} />
    <motion.li variants={item} />
    <motion.li variants={item} />
  </motion.ul>
);
```

## Orchestraction

- 기본적으로 모든 애니메이션은 동시에 시작한다.
- variants를 사용하면 when, delayChildren, staggerChildren과 같은 추가적은 transition props 값을 설정할 수 있다.
- 이를 통해 부모가 자식의 애니메이션을 조율할 수 있다.

## Dynamic variants

- 각 variant는 함수로 정의될 수 있다.
- variant 함수는 하나의 인자를 제공하는데, 이는 컴포넌트의 custom props로 전달된다.

```jsx
const variants = {
  visible: (i) => ({
    opacity: 1,
    transition: {
      delay: i * 0.3,
    },
  }),
  hidden: { opacity: 0 },
};

return items.map((item, i) => (
  <motion.li custom={i} animate="visible" variants={variants} />
));
```

## Multiple variants

- animate, whileHover와 같은 props는 여러개의 variants 값으로 이루어질 수 있다.
- 문자열 배열 형식
- 여러개의 variants가 발현되는 경우, 배열의 인덱스가 큰 variants 애니메이션부터 수행된다.

```jsx
<motion.ul variants={["open", "primary"]} />
```

## 수동 조작

- 대부분의 UI 인터렉션을 위해 선언적인 애니메이션이 이상적이지만, 때때로 복잡한 구현의 경우 다른 방식을 취할 수 있다.
- useAnimate hook
  - HTML/SVG 엘리먼트에 애니메이션 효과를 줄 수 있다.
  - 복잡한 애니메이션 효과를 줄 수 있다.
  - time, speed, play(), pause()등으로 에니메이션을 조작할 수 있다.

```jsx
const MyComponent = () => {
  const [scope, animate] = useAnimate();

  useEffect(() => {
    const animation = async () => {
      await animate(scope.current, { x: "100%" });
      animate("li", { opacity: 1 });
    };

    animation();
  }, []);

  return (
    <ul ref={scope}>
      <li />
      <li />
      <li />
    </ul>
  );
};
```

## Animate single values

## Animate content

## Hardward-accelerated animations
