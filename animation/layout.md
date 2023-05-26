## Layout 애니메이션

- css 레이아웃은 애니메이션화하기 어렵고 비용이 많이 든다.
- 높이를 100px에서 500px로 늘리는 애니메이션은 개념적으로 간단하지만 매 애니메이션 프레임마다 브라우저 레이아웃 시스템을 트리거하기 때문에 성능이 저하된다.
- framer motion은 레이아웃 시스템 대신 고성능의 transform 애니메이션을 사용하여 레이아웃 애니메이션을 구현한다.
- transform 속성은 reflow와 repaint를 거치지 않는다.
- layout 애니메이션을 사용하려면 motion 컴포넌트의 props로 layout을 주면 된다.
```jsx
<motion.div layout />
```