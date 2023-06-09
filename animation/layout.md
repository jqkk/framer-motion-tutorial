## Layout 애니메이션

- css 레이아웃은 애니메이션화하기 어렵고 비용이 많이 든다.
- 높이를 100px에서 500px로 늘리는 애니메이션은 개념적으로 간단하지만 매 애니메이션 프레임마다 브라우저 레이아웃 시스템을 트리거하기 때문에 성능이 저하된다.
- framer motion은 레이아웃 시스템 대신 고성능의 transform 애니메이션을 사용하여 레이아웃 애니메이션을 구현한다.
- transform 속성은 reflow와 repaint를 거치지 않는다.
- layout 애니메이션을 사용하려면 motion 컴포넌트의 props로 layout을 주면 된다.
```jsx
<motion.div layout />
```

## 크기 수정
- 모든 레이아웃 애니메이션은 `transform` 프로퍼티를 사용하여 수행된다.
- `transform`를 사용한 레이아웃 애니메이션은 자식 엘리먼트를 시각적으로 왜곡할 수도 있다.
- 이러한 왜곡을 수정하기 위해 요소의 첫번째 자식 요소에도 `layout`프로퍼티를 지정할 수 있다.

## 스크롤 컨테이너 안에서의 애니메이션
- 스크롤 컨테이너 안에서의 애니메이션은 적용하려면 해당 element에 `layoutScroll` 프로퍼티를 지정해야 한다.
```jsx
<motion.div
  layoutScroll
  style={{ overflow: "scroll" }}
/>
```

## 레이아웃 애니메이션 그룹핑
- `LayoutGroup`를 래핑하여 여러 구성 요소 간에 레이아웃 변경 사항을 동기화할 수 있다.
```jsx
import { LayoutGroup } from "framer-motion"

function List() {
  return (
    <LayoutGroup>
      <Accordion />
      <Accordion />
    </LayoutGroup>  
  )
}
```

## 공유된 레이아웃 애니메이션
```jsx
isSelected && <motion.div layoutId="underline" />
```