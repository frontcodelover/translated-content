---
title: 반응형 디자인
slug: Learn/CSS/CSS_layout/Responsive_Design
l10n:
  sourceCommit: c51e0599ea09c0e6d035c635db9f48ad1f241490
---

{{learnsidebar}}{{PreviousMenuNext("Learn/CSS/CSS_layout/Multiple-column_Layout", "Learn/CSS/CSS_layout/Media_queries", "Learn/CSS/CSS_layout")}}

반응형 웹 설계 는 웹 페이지가 모든 화면 크기와 해상도에서 잘 렌더링되도록 하면서도 사용성을 보장하는 웹 디자인 접근 방식입니다. 멀티 디바이스 웹을 위한 디자인 방식입니다. 이 글에서는 이를 숙달하기 위해 사용할 수 있는 몇 가지 기술을 이해하는 데 도움이 될 것입니다.

<table>
  <tbody>
    <tr>
      <th scope="row">필요한 사전 지식:</th>
      <td>
        HTML의 기초인 (<a
          href="/ko/docs/Learn/HTML/Introduction_to_HTML"
          >HTML 입문서</a
        >를 공부하세요), 그리고 CSS의 작동 방식을 파악하기 위해 (<a
          href="/ko/docs/Learn/CSS/First_steps"
          >CSS 첫걸음</a
        >과
        <a href="/ko/docs/Learn/CSS/Building_blocks">CSS 구성 블록</a>를
        공부하세요.)
      </td>
    </tr>
    <tr>
      <th scope="row">목표:</th>
      <td>반응형 디자인의 역사와 핵심적인 개념 파악하기</td>
    </tr>
  </tbody>
</table>

HTML은 기본적으로 반응형 또는 유동적 입니다. CSS 없이 HTML만 포함된 웹 페이지를 만들고 창 크기를 조정하면 브라우저는 뷰포트에 맞게 텍스트를 자동으로 리플로우합니다.

기본 반응형 동작은 별다른 해결책이 필요하지 않은 것처럼 보일 수 있지만 와이드 모니터에서 전체 화면으로 표시되는 긴 텍스트 줄은 읽기 어려울 수 있습니다. 열을 만들거나 패딩을 크게 추가하는 등 CSS를 사용하여 와이드 스크린 줄 길이를 줄이면 브라우저 창을 좁히거나 모바일 장치에서 사이트를 여는 사용자에게 사이트가 찌그러져 보일 수 있습니다.

![두 개의 열이 있는 레이아웃이 모바일 크기 뷰포트에서 찌부러집니다.](mdn-rwd-liquid.png)

고정 너비를 설정하여 크기를 조정할 수 없는 웹 페이지를 만들면 좁은 기기에서는 스크롤 막대가 나타나고 넓은 화면에서는 빈 공간이 너무 많아집니다.

반응형 웹 디자인(RWD)은 다양한 디바이스와 디바이스 크기에 대응하는 디자인 접근 방식으로, 태블릿, 휴대폰, 텔레비전, 시계 등 어떤 디바이스에서 콘텐츠를 보든 화면에 맞게 자동으로 조정할 수 있습니다.

반응형 웹 디자인은 별도의 기술이 아니라 하나의 접근 방식입니다. 콘텐츠를 보는 데 사용되는 모든 기기에 대응할 수 있는 레이아웃을 만드는 데 사용되는 일련의 모범 사례를 설명하는 데 사용되는 용어입니다.

반응형 디자인이라는 용어는 [2010년 Ethan Marcotte가 만든 것](https://alistapart.com/article/responsive-web-design/)으로, Zoe Mickley Gillenwater의 저서 [Flexible Web Design](http://flexiblewebbook.com/)에서 설명한 대로 유동 그리드, 유동 이미지, 미디어 쿼리를 사용하여 반응형 콘텐츠를 만드는 것을 설명합니다.

당시에는 레이아웃 및 미디어 쿼리에 CSS `float`를 사용하여 브라우저 너비를 쿼리하고 다양한 분기점에 대한 레이아웃을 생성하는 것이 권장되었습니다. Fluid 이미지는 컨테이너 너비를 초과하지 않도록 설정되며, `max-width` 속성이 `100%`로 설정되어 있습니다. Fluid 이미지는 포함 열이 좁아지면 축소되지만 열이 커질 때 고유 크기보다 커지지 않습니다. 이렇게 하면 컨테이너가 이미지보다 넓어져도 이미지가 넘치지 않고 콘텐츠에 맞게 축소되지만 더 커지거나 픽셀화되지 않습니다.

최신 CSS 레이아웃 방식은 본질적으로 반응형이며, Gillenwater의 책과 Marcotte의 글이 출간된 이후 반응형 사이트를 더 쉽게 디자인할 수 있도록 웹 플랫폼에 다양한 기능이 내장되어 있습니다.

이 글의 나머지 부분에서는 반응형 사이트를 만들 때 사용할 수 있는 다양한 웹 플랫폼 기능을 소개합니다.

## 미디어 쿼리

[미디어 쿼리 사용하기](/ko/docs/Web/CSS/CSS_media_queries/Using_media_queries)를 사용하면 일련의 테스트(예: 사용자의 화면이 특정 너비 또는 특정 해상도보다 큰지 여부)를 실행하고 CSS를 선택적으로 적용하여 사용자의 요구에 맞게 페이지의 스타일을 지정할 수 있습니다.

예를 들어, 다음 미디어 쿼리는 현재 웹 페이지가 화면 미디어로 표시되고 있고(따라서 인쇄된 문서가 아님) 뷰포트의 너비가 `80rem` 이상인지 테스트합니다. `.container` 선택기에 대한 CSS는 이 두 가지가 참인 경우에만 적용됩니다.

```css
@media screen and (min-width: 80rem) {
  .container {
    margin: 1em 2em;
  }
}
```

스타일시트 내에 여러 미디어 쿼리를 추가하여 다양한 화면 크기에 가장 적합하도록 전체 레이아웃 또는 일부를 조정할 수 있습니다. 미디어 쿼리가 도입되고 레이아웃이 변경되는 지점을 _breakpoints_(분기점)라고 합니다.

미디어 쿼리를 사용할 때 일반적인 접근 방식은 화면이 좁은 디바이스(예: 휴대폰)를 위해 간단한 단일 열 레이아웃을 만든 다음 화면이 더 넓은지 확인하고 화면 너비가 충분하다고 판단되면 다중 열 레이아웃을 구현하는 것입니다. 이를 **모바일 우선** 디자인이라고 합니다.

분기점을 사용하는 경우, 개별 디바이스의 절대 크기보다는 [CSS 값과 단위](/ko/docs/Learn/CSS/Building_blocks/Values_and_units#상대_길이_단위)를 사용하여 미디어 쿼리 분기점을 정의하는 것이 모범 사례입니다.

미디어 쿼리 블록 내에 정의된 스타일에 대한 접근 방식은 브라우저 크기 범위에 따라 {{htmlelement("link")}} 스타일 시트에 미디어 쿼리를 사용하는 것부터 각 분기점과 관련된 값을 저장하기 위해 사용자 지정 속성 변수만 포함하는 것까지 다양합니다.

[미디어 쿼리](/ko/docs/Web/CSS/Media_Queries)에 대한 MDN 문서를 더 찾아보십시요.

## 반응형 레이아웃 기술

반응형 사이트는 유연한 그리드를 기반으로 구축되므로 픽셀 단위의 완벽한 레이아웃으로 가능한 모든 기기 크기를 타겟팅할 필요가 없습니다.

유연한 그리드를 사용하면 기능을 변경하거나 분기점을 추가하여 콘텐츠가 보기 좋지 않게 보이는 지점에서 디자인을 변경할 수 있습니다. 예를 들어 화면 크기가 커짐에 따라 줄 길이가 읽기 힘들 정도로 길어지지 않도록 {{cssxref('columns')}}를 사용할 수 있으며, 상자가 좁아지면서 각 줄에 두 단어가 찌그러지는 경우 분기점을 설정할 수 있습니다.

[다단 레이아웃](/ko/docs/Learn/CSS/CSS_layout/Multiple-column_Layout), [Flexbox](/ko/docs/Learn/CSS/CSS_layout/Flexbox), [그리드](/ko/docs/Learn/CSS/CSS_layout/Grids) 등 여러 레이아웃 방식이 기본적으로 반응형입니다. 모두 사용자가 유연한 그리드를 만들려고 한다고 가정하고 더 쉬운 방법을 제공합니다.

### 다단

다단을 사용하면 콘텐츠를 분할할 최대 열 수를 나타내는 `column-count`를 지정할 수 있습니다. 그러면 브라우저에서 화면 크기에 따라 변경되는 크기를 계산합니다.

```css
.container {
  column-count: 3;
}
```

`column-width`을 지정하는 대신 _minimum_ 너비를 지정하는 것입니다. 브라우저는 컨테이너에 편안하게 들어갈 수 있는 만큼 해당 너비의 열을 생성한 다음 모든 열 사이에 남은 공간을 공유합니다. 따라서 열의 수는 공간의 양에 따라 변경됩니다.

```css
.container {
  column-width: 10em;
}
```

{{cssxref('columns')}} 단축키를 사용하여 최대 열 수와 최소 열 너비를 지정할 수 있습니다. 이렇게 하면 화면 크기가 커짐에 따라 줄 길이가 읽기 힘들 정도로 길어지거나 화면 크기가 작아짐에 따라 너무 좁아지는 것을 방지할 수 있습니다.

### 플렉스박스

플렉스박스에서 플렉스 항목은 컨테이너의 공간에 따라 항목 사이의 공간을 분배하여 축소 또는 증가합니다. `flex-grow` 및 `flex-shrink` 값을 변경하여 주변에 공간이 많거나 적을 때 항목이 어떻게 동작할지 지정할 수 있습니다.

아래 예시에서 플렉스 항목은 레이아웃 항목 [플렉스박스: 가변 항목의 가변 크기 조정](/ko/docs/Learn/CSS/CSS_layout/Flexbox#가변_항목의_가변_크기_조정)에 설명된 대로 `flex: 1`의 약어를 사용하여 플렉스 컨테이너에서 각각 동일한 공간을 차지합니다.

```css
.container {
  display: flex;
}

.item {
  flex: 1;
}
```

> [!NOTE]
> 예를 들어, 플렉스박스를 사용하여 위의 간단한 반응형 레이아웃을 만들었습니다. 화면이 커지면 중단점을 사용하여 여러 열로 전환하고 {{cssxref('max-width')}}로 메인 콘텐츠의 크기를 제한합니다. [예시](https://mdn.github.io/css-examples/learn/rwd/flex-based-rwd.html), [소스 코드](https://github.com/mdn/css-examples/blob/main/learn/rwd/flex-based-rwd.html).

### CSS 격자

CSS 그리드 레이아웃에서 `fr` 단위는 그리드 트랙에 사용 가능한 공간을 분배할 수 있게 해줍니다. 다음 예제는 `1fr` 크기의 트랙 3개가 있는 그리드 컨테이너를 생성합니다. 이렇게 하면 컨테이너에서 사용 가능한 공간의 한 부분을 차지하는 세 개의 열 트랙이 생성됩니다. 그리드를 만드는 이 접근 방식에 대한 자세한 내용은 레이아웃 그리드 배우기 주제의 [fr 단위를 포함한 가변 격자](/ko/docs/Learn/CSS/CSS_layout/Grids#fr_단위를_포함하는_가변_격자) 아래에서 확인할 수 있습니다.

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```

> [!NOTE]
> 격자 레이아웃 버전은 .wrapper [예제](https://mdn.github.io/css-examples/learn/rwd/grid-based-rwd.html)상에 열을 정의할 수 있으므로 더 간단합니다: [소스 코드](https://github.com/mdn/css-examples/blob/master/learn/rwd/grid-based-rwd.html).

## 반응형 이미지

미디어가 반응형 컨테이너보다 크지 않도록 하려면 다음과 같은 방법을 사용할 수 있습니다.

```css
img,
picture,
video {
  max-width: 100%;
}
```

이렇게 하면 미디어가 컨테이너를 넘치지 않도록 크기를 조정합니다. 하나의 큰 이미지를 사용했다가 작은 디바이스에 맞게 축소하면 필요한 것보다 큰 이미지를 다운로드하여 대역폭이 낭비됩니다.

반응형 이미지는 {{htmlelement("picture")}}와 {{htmlelement("img")}} 요소, `srcset` 및 `sizes` 속성을 사용해 사용자의 뷰포트와 디바이스의 해상도에 맞는 이미지를 제공할 수 있습니다. 예를 들어 모바일용 정사각형 이미지를 포함할 수 있지만 데스크톱에서는 가로 이미지와 동일한 장면을 표시할 수 있습니다.

`<picture>` 요소를 사용하면 "hints"(이미지가 가장 적합한 화면 크기 및 해상도를 설명하는 메타데이터)와 함께 여러 크기를 제공할 수 있으며, 브라우저는 각 디바이스에 가장 적합한 이미지를 선택하므로 사용자가 사용 중인 디바이스에 적합한 이미지 크기를 다운로드할 수 있습니다. `max-width`와 함께 `<picture>`을 사용하면 미디어 쿼리로 이미지 크기를 조정할 필요가 없습니다. 이는 다른 화면비의 이미지를 다른 뷰포트 크기에 맞추어 사용할 수 있도록 합니다.

또한 다양한 크기로 사용되는 이미지를 직접 _art direct_ 하여 화면 크기에 따라 다른 자르기 또는 완전히 다른 이미지를 제공할 수도 있습니다.

이곳 MDN 사이트의 [반응형 이미지](/ko/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images)에서 자세한 안내서를 찾을 수 있습니다.

## 반응형 타이포그래피

반응형 타이포그래피는 미디어 쿼리 내에서 글꼴 크기를 변경하거나 뷰포트 단위를 사용하여 화면 공간을 더 적게 또는 더 많이 반영하는 것을 설명합니다.

### 반응형 타이포그래피에 대한 미디어 쿼리 사용하기

이 예제에서 우리는 수준 1 머리글을 `4rem`로 설정하려고 합니다. 즉, 기본 글꼴 크기의 4배입니다. 정말 큰 제목이네요! 이 커다란 제목은 더 큰 화면 크기에서만 사용해야 하므로 먼저 더 작은 제목을 만든 다음 사용자의 화면 크기가 `1200px` 이상인 경우 미디어 쿼리를 사용하여 더 큰 크기로 덮어씁니다.

```css
html {
  font-size: 1em;
}

h1 {
  font-size: 2rem;
}

@media (min-width: 1200px) {
  h1 {
    font-size: 4rem;
  }
}
```

위의 반응형 그리드 예시를 편집하여 설명한 방법을 사용하여 반응형 유형도 포함하도록 했습니다. 레이아웃이 두 열 버전으로 전환됨에 따라 제목의 크기가 어떻게 전환되는지 확인할 수 있습니다.

모바일에서는 제목이 더 작아집니다.

![머리글 크기가 작은 스택 모양의 레이아웃입니다.](mdn-rwd-font-mobile.png)

그러나 데스크톱에서는 제목 크기가 더 크게 표시됩니다.

![큰 머리글이 딸린 두개의 열 레이아웃입니다.](mdn-rwd-font-desktop.png)

> [!NOTE]
> 이 예제의 실제 구현 장면: [예제](https://mdn.github.io/css-examples/learn/rwd/type-rwd.html), [소스 코드](https://github.com/mdn/css-examples/blob/master/learn/rwd/type-rwd.html).

타이포그래피에 대한 이 접근 방식에서 알 수 있듯이 미디어 쿼리를 페이지 레이아웃 변경에만 제한할 필요는 없습니다. 모든 요소를 조정하여 다른 화면 크기에서 더 유용하거나 매력적으로 보이도록 하는 데 사용할 수 있습니다.

### 반응형 타이포그래피에 대한 뷰포트 단위 사용하기

뷰포트 단위 `vw`를 사용하여 미디어 쿼리로 중단점을 설정할 필요 없이 반응형 타이포그래피를 활성화할 수도 있습니다. `1vw`는 뷰포트 너비의 1%에 해당하므로 `vw`를 사용하여 글꼴 크기를 설정하면 항상 뷰포트의 크기와 관련됩니다.

```css
h1 {
  font-size: 6vw;
}
```

위와 같이 할 때의 문제점은 텍스트가 항상 뷰포트의 크기와 관련되어 있기 때문에 사용자가 'vw' 단위를 사용하여 설정한 텍스트를 확대/축소할 수 없다는 것입니다. **따라서 뷰포트 단위만 사용하여 텍스트를 설정해서는 안 됩니다**.

해결책이 있는데, [`calc()`](/ko/docs/Web/CSS/calc)를 사용하는 것입니다. `em` 또는 `rem`과 같은 고정 크기를 사용하여 설정된 값에 `vw` 단위를 추가하면 텍스트를 계속 확대/축소할 수 있습니다. 기본적으로 `vw` 단위는 확대된 값 위에 추가됩니다.

```css
h1 {
  font-size: calc(1.5rem + 3vw);
}
```

즉, 모바일용으로 설정하고 미디어 쿼리에서 다시 정의할 필요 없이 제목의 글꼴 크기를 한 번만 지정하면 됩니다. 그런 다음 뷰포트의 크기를 늘리면 글꼴이 점차 커집니다.

> [!NOTE]
> 이에 대한 예제의 실현: [예제](https://mdn.github.io/css-examples/learn/rwd/type-vw.html), [소스 코드](https://github.com/mdn/css-examples/blob/main/learn/rwd/type-vw.html).

## 뷰포트 메타 테그

반응형 페이지의 HTML 소스를 보면 일반적으로 문서의 `<head>`에 다음과 같은 {{htmlelement("meta")}} 태그를 볼 수 있습니다.

```html
<meta name="viewport" content="width=device-width,initial-scale=1" />
```

이 [viewport](/ko/docs/Web/HTML/Viewport_meta_tag) 메타 태그는 모바일 브라우저에 뷰포트의 너비를 기기 너비로 설정하고 문서의 크기를 의도한 크기의 100%로 조정하여 문서를 모바일에 최적화된 크기로 표시해야 함을 알려줍니다.

이것이 왜 필요한가요? 모바일 브라우저는 뷰포트 너비에 대해 거짓말을 하는 경향이 있기 때문입니다.

이 메타 태그가 존재하는 이유는 스마트폰이 처음 등장했을 때 대부분의 사이트가 모바일에 최적화되지 않았기 때문입니다. 따라서 모바일 브라우저는 뷰포트 너비를 980픽셀로 설정하고 해당 너비로 페이지를 렌더링한 후 데스크톱 레이아웃의 축소된 버전으로 결과를 표시했습니다. 사용자는 웹사이트를 확대하고 이동하면서 관심 있는 부분을 볼 수 있었지만 보기가 좋지 않았습니다.

`width=device-width`를 설정하면 Apple의 기본값인 `width=980px`와 같은 모바일 디바이스의 기본값을 디바이스의 실제 너비로 재정의하게 됩니다. 이 설정이 없으면 중단점 및 미디어 쿼리가 포함된 반응형 디자인이 모바일 브라우저에서 의도한 대로 작동하지 않을 수 있습니다. 뷰포트 너비가 480픽셀 이하인 좁은 화면 레이아웃이 있는데 기기에서 980픽셀 너비라고 표시되는 경우 해당 사용자는 좁은 화면 레이아웃을 볼 수 없습니다.

**따라서 문서 헤드에 뷰포트 메타 태그를 항상 포함해야 합니다.**

## 요약 정리

반응형 디자인이란 보는 환경에 따라 반응하는 사이트 또는 애플리케이션 디자인을 말합니다. 반응형 디자인은 여러 CSS 및 HTML 기능과 기술을 포함하며, 이제는 기본적으로 웹사이트를 구축하는 방식이 되었습니다. 휴대폰으로 방문하는 사이트를 생각해 보세요. 데스크톱 버전이 축소되어 있거나 옆으로 스크롤해야 무언가를 찾을 수 있는 사이트를 접하는 것은 매우 드문 일입니다. 이는 웹이 반응형 디자인 방식으로 전환되었기 때문입니다.

또한 이번 단원에서 배운 레이아웃 방법을 사용하면 반응형 디자인을 훨씬 쉽게 구현할 수 있습니다. 오늘날 웹 개발이 처음이라면 반응형 디자인 초창기보다 더 많은 도구를 사용할 수 있습니다. 따라서 사용 중인 자료의 연도를 확인하는 것이 좋습니다. 과거의 자료는 여전히 유용하지만, 최신 CSS와 HTML을 사용하면 방문자가 어떤 디바이스로 사이트를 보든 우아하고 유용한 디자인을 훨씬 쉽게 만들 수 있습니다.

## 같이 보기

- [미디어 쿼리에 대한 CSS 요령 가이드](https://css-tricks.com/a-complete-guide-to-css-media-queries/)

{{PreviousMenuNext("Learn/CSS/CSS_layout/Multiple-column_Layout", "Learn/CSS/CSS_layout/Media_queries", "Learn/CSS/CSS_layout")}}