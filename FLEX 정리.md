### **FLEX 정리**

자료 - 생활코딩

FLEX를 사용하기 위해선 두 종류의 태그가 필요함.

컨테이너역할을 하는 container 태그와 자식 역할을 하는 item태그(정렬의대상이되는)가 있어야함.



**아래는 컨테이너 태그와 아이템 태그에 부여할수 있는 속성**

![](https://ws2.sinaimg.cn/large/006tKfTcgy1fhw1xj9s4kj30qk0h4dgu.jpg)

#### 예제 0. flex-direction

- flex-direction 아무것도 설정안하면? row 속성
- row-reverse 는 가로를 기준으로 역순 정렬
- culumn 속성과 culumn-reverse 속성도 존재!

```html
<!doctype>
<html>
<head>
    <style>
        .container {
            background-color: powderblue;
            height:200px;
            display: flex;
            flex-direction: row;
        }
        .item {
            background-color: tomato;
            color:white;
            border: 1px solid white;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>


```

#### 예제 1. flex-grow, flex-basis, flex-shrink

- flex-grow 를 1로 설정하면 다섯개의 item 들이 컨테이너를 5등분 해서 나눠가진다.
- flex-shrink를 0으로 설정하면 화면이 작아져도 item 의 크기는 줄어들지않는다.
- flex-basis는 flex 각 아이템들의 기본크기를 설정한다.

```html
<!doctype>
<html>
<head>
    <style>
        .container{
            background-color: powderblue;
            height:200px;
            display:flex;
            flex-direction:row;
        }
        .item{
            background-color: tomato;
            color:white;
            border:1px solid white;         
        }
        .item:nth-child(1){
            flex-basis: 150px;
            flex-shrink: 1;
        }
        .item:nth-child(2){
            flex-basis: 150px;
            flex-shrink: 2;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="item">1</div>
        <div class="item">2</div>
        <div class="item">3</div>
        <div class="item">4</div>
        <div class="item">5</div>
    </div>
</body>
</html>
```

#### 예제 2. HolyGrailLayout

```html
<!doctype>
<html>
<head>
    <meta charset="utf-8">
    <style>
        .container{
            display: flex;
            flex-direction: column;
        }
        header{
            border-bottom:1px solid gray;
            padding-left:20px;
        }
        footer{
            border-top:1px solid gray;
            padding:20px;
            text-align: center;
        }
        .content{
            display:flex;
        }
        .content nav{
            border-right:1px solid gray;
        }
        .content aside{
            border-left:1px solid gray;    
        }
        nav, aside{
            flex-basis: 150px;
            flex-shrink: 0;
        }
        main{
            padding:10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>생활코딩</h1>
        </header>
        <section class="content">
            <nav>
                <ul>
                    <li>html</li>
                    <li>css</li>
                    <li>javascript</li>
                </ul>
            </nav>
            <main>
                Lorem ipsum dolor sit amet, consectetur adipisicing elit. Reiciendis veniam totam labore ipsum, nesciunt temporibus repudiandae facilis earum, sunt autem illum quam dolore, quae optio nemo vero quidem animi tempore aliquam voluptas assumenda ipsa voluptates. Illum facere dolor eos, corporis nobis, accusamus velit, similique cum iste unde vero harum voluptatem molestias excepturi. 
            </main>
            <aside>
                AD
            </aside>
        </section>
        <footer>
            <a href="https://opentutorials.org/course/1">홈페이지</a>
        </footer>
    </div>
</body>
</html>
```

#### 그외 기타속성들 

https://opentutorials.org/course/2418/13526



