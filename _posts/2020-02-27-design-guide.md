---
title: "[design] Web Design Guide"
layout: post
date: 2020-02-27
author: wnsgur
tags: design
comments: true
---

> 웹 페이지를 개발하다 보면 항상 궁금했던 점이 있었다.   
> margin과 padding은 얼만큼 주어야 클라이언트들이 보기 편할까? 레이아웃은 어떻게 잡아야할까?
> 사실 이런 고민들은 디자인 관점이 더 컸기에, 나한테 미숙했던 부분들이였다.
> 그래서 관심을 갖고 자료를 찾던 와중에 좋은 유튜브와 웹 사이트를 알게 되었다.
> 자료를 바탕으로 개발자로서 알아두면 좋은 tip(?)들을 정리하기로 했다.

# 참고
- [Remain style guide](http://styleguide.co.kr/content/resolution-grid/ratio-design.php)
- [김성혜님 behance](https://www.behance.net/gallery/65390457/Graphic-Guide)

# 1. 이미지 비율
1:1 / 2:1 / 3:2 / 4:3 / 16:9 비율이 시각적인 안정감을 준다.

# 2. Spacing system
8배수의 규칙을 세워서 여백을 주면, 전체적인 안정감과 통일감을 줄 수 있다.
8px / 16px / 24px / 32px / 40px / 48px / 56px

또는

4배수에 기반한 6가지 단위
xxs/4px, xs/8px, sm/16px, md/20px, lg/40px, xl/60px


# 3. Grid System
![](http://styleguide.co.kr/content/resolution-grid/responsive-grid-imgs/grid_ex17.png)

- 그리드 시스템은 일관성, 체계적 배열을 도와줍니다.
- Column(실제 컨텐츠 부분), Gutter(컬럼과 컬럼 사이 여백), Margin(가장자리, 왼쪽과 오른쪽)으로 구성됩니다.

- 모바일의 경우
    - 4column, 6column 등 여러 가지를 사용하지만, `6column`을 사용함.
    - 그 이유는, 2분할과 3분할을 적용할 수 있기때문

- 웹의 경우
 - 15column과 12column을 사용
 - 참고로 bootstrap은 12column
 

# 4. font size
14 / 16 / 20 / 24 / 32 / 40
[css font 환산 사이트](http://pxtoem.com/) 꼭 참조 바람!

# 5. font weight
글자의 굵기를 잘 활용하자.
thin / regular / bold

# 6. line-height
행간은 보통 font-size * 1.5로 계산하여 사용

# 7. button
활성 / 비활성화 / 행동을 고려하여 디자인 하기.

# 8. Tab
최소 3개 이상의 컨텐츠가 존재할 때 사용!

# 9. 해상도에 따른 배율 디자인
보통 8배수를 사용한다고 한다.
이유는 1.5배, 0.5배 등 소수점에도 대응이 가능하며, 4배수는 기본적으로 크기가 작기때문이라고 한다....
[참고](http://styleguide.co.kr/content/resolution-grid/ratio-design.php) 하시길 바랍니다.






