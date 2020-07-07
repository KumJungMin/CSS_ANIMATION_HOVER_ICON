# 설명 박스, hover시 변하는 애니메이션

## 1. preview

<img src="https://j.gifs.com/mOmL1G.gif" />


## 2. 코드 분석

### 1) html
- `<div class="container">` : 내부 요소를 감싸는 부모 요소이다.
- `<div class="icon">` : `container`의 자식요소, 이미지와 글자의 부모요소이다.
- `<span>` : 아이콘에 마우스를 hover했을 때 말풍선으로 쓰일 태그이다.


#### (1) icon클래스에서 img, span 요소를 자식요소로 한다.
```html
<body>
    <div class="container">
        <div class="icon">
            <img class="img1" src=""/>
            <span>이 아이콘에 대한 설명입니다.!</span>
        </div>
    </div>
</body>
```

<br/><br/>

### 2) css

#### (1) icon의 자식인 span태그 설정
- 중앙배치 

  : 부모요소의 `pistion을 relative`, span의 `pistion을 absolute`으로 둔다.
  
  : `left를 50%`을 설정하고 왼쪽에서 50%위치에 둔다.
  
  : `transform을 translateX(-50%)`로 설정하여, X크기값을 50%만큼 이동시켜준다.
  
  : 결과적으로 화면 크기가 변해도 항상 중앙에 위치하게 된다.
  
<br/>

- `span`에 이벤트 설정

  : 서서히 나타나게 하려면 `display:none->block`보다는 `opacity:0->1`으로 두는게 더 효과가 좋음

  : `visibility: hidden`을 하면 자릿값을 유지하되, 눈에 보이지 않게 할 수 있다.(`display:none`은 자릿값도 사라지게 함)

<br/>

- 특정 요소에 `hover`했을 때만 이벤트 발생시키기

  : 사용자가 아이콘이 아닌, 말풍선이 있는 위치에 마우스를 올려도 효과가 발생!

  : 그렇다면 말풍선의 존재 자체를 없게 만들면 됨 -> `visiability`를 이용한다. (display를 하면 투명도를 못 줌ㅜ)
       
<br/>

```css

 .icon {
        width: 110px;         /*전체를 감싸는 크기를 아이콘 크기로 맞춤*/
        height: 110px;
        margin: 10px;
        position: relative;
    }
    .icon span{
        position: absolute;  /*어떤 요소에 absolute를 주면 블럭요소는 inline으로 변경됨.*/
        background-color: #000;
        width: 200px;
        color : #fff;
        top : -80px;
        text-align: center;
        padding: 10px;
        border-radius: 5px;
        left: 50%;                    /*중앙배치 : 왼쪽에서 50%위치*/
        transform: translateX(-50%);  /*중앙배치 : X크기값을 50%만큼 이동*/
        opacity: 0;                   /*이벤트설정 : 서서히 변하게 함*/
        transition: 0.5s;             /*어떤 변화가 요청되면 0.5초뒤에 일어나자.*/

        
        visibility: hidden;          /*특정 요소 접촉시 이벤트 발생*/

    }

```

<br/>

#### (2) 가상클래스(before, after)를 사용해 요소 꾸미기 
- `span` 요소 아래에 있는 삼각형을 만들어보자

  : 먼저 사각형을 요소 끝에 만듬(`after`라는 가상클래스 사용)
  
  : 원하는 자리에 위치시키고 회전시킴(`transform: rotate(45deg) translateX(-50%)`)
  
  : 가상클래스를 `span`과 같은 색깔로 바꿈
  
  : 결과적으로 사각형이 회전하여 삼각형처럼 보임 
  
  <br/>
  
 - 가상 클래스 `after` 사용법
 
  : 선택한 요소의 맨 마지막 자식으로 의사 요소를 하나 생성한다.
  
  : 보통 `content` 속성과 함께 짝지어, 요소에 장식용 콘텐츠를 추가할 때 사용합니다. 기본값은 인라인이다.
  
  
  

```css

    .icon span:after {
        content : '';             /*가상클래스 before, after는 무조건 content가 있어야 작동*/
        position: absolute;       /*상위클래스icon이 relative이므로, absolute로 설정하여 동적페이지에도 같은 위치로 유지*/
        background-color:#000;
        width : 10px;
        height: 10px;
        transform: rotate(45deg) translateX(-50%);  /*transform은 한 요소에 1번밖에 못쓰므로 합쳐줘야함*/
        bottom: -5px;
        left: 50%;                                  /*1. 왼쪽에서 50%위치에 둔다.*/
                                                    /*2. 크기값을 50%만큼 이동시켜준다.->항상 중앙에 위치하게됨*/
    
    }
```

<br/>

#### (3) icon을 hover span 이벤트 발생 

- `.icon:hover span` :  icon요소를 hover하면, icon의 자식 중 span에서 어떠한 변화가 있게 만듬
- `visibility: visible` :hover가 되면 visibility가 hidden에서 visible로 변경됨(오직 아이콘에 hover했을 때 변경됨)

  
```css
    .icon:hover span{
        opacity: 1;
        visibility: visible;     /*hover시 발생하ㅡㄴ 이벤트*/
       
    }

    .container {
        text-align : center;     /*글자 중앙 정렬*/
        display: flex;           /*가로로 일렬 배치*/
        justify-content: center; /*수평 중앙*/
        align-items: center;     /*수직 중앙 -> container의 높이값이 있어야 적용됨*/
        height : 100vh;          
    }
    
    .img1{
        width : 100px;
        height: 100px;
    }

```










