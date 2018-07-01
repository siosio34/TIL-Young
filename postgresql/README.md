# Postgresql 정리

### 설치(ubuntu)

```
	$ sudo apt-get install postgresql
	$ service postgresql restart
```

### Sample 데이터 불러오기
[- (샘플데이터 다운로드)](http://www.postgresqltutorial.com/postgresql-sample-database/)
	
```
	$ su -u postgres
	$ psql
	$ CREATE DATABASE dvdrental;
	$ psql 터미널 창에서 나온후 pg_restore -U postgres -d dvdrental ${dvdrental.tar의 경로)
```

### sample 데이터 접속
```
	$ su - postgres
	$ psql -d dvdrental
```

#### 아래는 기존에 알던 부분이 아닌 나한테 생소한 부분만 따로 정리되어 있어서 전체 적인 설명은 [포스트그레스 튜도리얼](http://www.postgresqltutorial.com/) 을 참고한다.

##### OFFSET
```
- 주로 LIMIT와 함께 페이지네이션을 개발할때 주로 쓴다.
- SELECT * FROM film LIMIT 10 === SELECT  * FROM film LIMIT 10 OFFSET 0;
- SELECT * FROM flim LIMIT 10 OFFSET 10 (11번째부터 10개의 행을 반환한다)
```
##### FETCH
```
- LIMIT 랑 하는 역할이 비슷하다.
- SELECT * FROM film FETCH 5 ROW ONLY; (첫번째 행부터 5개의 행을 반환한다.)
```

##### IN
```
- 리스트 안의 값과 일차하는 값이 있는지 WHERE 문안에서 체크한다.
- SELECT * FROM rental WHERE customer_id NOT IN (1,2) => customer_id가 1또는 2가 아니면 가져온다.
```
##### LIKE
```
- %(다중 글자 매칭), _(단일 글자 매칭) 패턴과 함께 사용되어 string 을 비교하는데 사용된다.
- SELCT first_name FROM customer WHERE first_name 'BAR%' => BAR 로 시작하여 뒤에는 어떤글자로든 끝나든 상관없다.
- 대소문자를 구별하며 구별하지않으려면 ILIKE를 사용한다. 

```
##### INNER JOIN
```
- 교집합이라고 생각하면 편하다.
- SELECT * FROM customer INNER JOIN payment ON payment.customer_id = customer.customer_id; (custommer 테이블과 payment 테이블을 조인하는데 custommer id 가 서로 같은 행만 조인한다.)
```
##### LEFT JOIN
```
- 왼쪽 테이블이 기준이 된다.
- 왼쪽 테이블 row 와 조건에 맞는 오른쪽 테이블 row가 없어도 오른쪽 테이블에서 값만 안가져올뿐이지 왼쪽 테이블에 있는 내용을 출력한다. 
- SELECT A.pka, A.c1, B.pkb B.c2 FROM A LEFT JOIN B ON A.pka = B.pka => pka 정보가 맞는 경우 B.pkb 와 B.c2 정보를 들고와서 row를 그려주고 없다하더라도 row 에 A의 데이터만 넣어서 그려준다.
```

##### RIHGT JOIN
```
- 오른쪽이 기준이 될뿐이지 LEFT JOIN 이랑 개념은 유사하다.
```
##### SELF JOIN
```
- 같은 테이블 내끼리 JOIN 하는것, 같은 테이블내에 값을 비교하는데 좋음. 
- SELECT e.first_name || ' ' || e.last_name,
m .first_name || ' ' || m .last_name manager
FROM employee m on m .employee_id = e.manager_id
(같은 테이블내 직원아이디가 매니저 아이디인사람만 출력한다.)

```
##### FULL OUTER JOIN
```
- LEFT JOIN과 RIGHT JOIN 의 결과를 합친것이다.
- JOIN 조건에 맞지 않아도 한쪽에만 있는 값을 가져오고 다른쪽에 있는값을 NULL 로 처리해 가져온다.
- SELECT name FROM employee e FULL OUTER JOIN depratments d ON d.department_id = e.department_id => id가 일치하는행 + id 가 일치하지않더라도 A,B 가 가지고 있는값 + 없는값은 NULL 로 가져와 보여준다.

```
##### CROSS JOIN
```
- LEFT JOIN 과 INNER JOIN 과 다르게 조인문 안에 조건문이 들어가지 않는다.
- SELECT * FROM T1 CROSS JOIN TW; === SELECT * FROM T1,T2 === SELECT * FROM T1 INNER JOIN T2 ON TRUE (위 세개가 모드 같은 구문이다.)
- A가 항목이 2개 B 가 항목이 3개인경우 총 6개의 항목이 만들어진다.

```
##### NATURAL JOIN
```
- 같은 COLUMN 이름이 기반하여 테이블을 조인함. 기본은 INNER JOIN이다.
- SELECT * FROM producs NATURAL JOIN categories; === SELECT * FROM products INNER JOIN categories USING (category_id)
- 예기치 못한 결과를 초래하므로 사용을 피해야한다.(어지간하면 INNER JOIN 에 조건을 명시하여 사용한다.)
```
##### GROUP BY
```
- row들을 SELECT 한 열(속성)의 그룹들로 나눈다.
- SUM 같은 FUNCTION 들과 같이 써서 그룹에 특정 열의 합을 구하는데도 자주쓰인다.
- SELECT customer_id, SUM (amount) FROM paymeSnt GROUP BY customer_id ORDER BY SUM (amount) DESC; => customer_id를 기준으로 그룹으로 묶고 그 구룹의 amout 의 총량을 구한뒤 그걸 기준으로 내림차순 정렬한다.

```
##### HAVING
```
- GROUP by 랑 같이 조건에 맞지않은 행을 필터링 하기위해서 사용한다.
- SELECT customer_id, SUM (amount) FROM payment GROUP BY customer_id HAVING SUM (amount) > 300; => customer_id 를 기준으로 그룹화하는데 그중 amount 의 총량이 300 초과인것만 리턴한다.
```
##### UNION
```
- 여러 쿼리들의 결과셋을 하나의 결과셋으로 합쳐주는 쿼리이다.
- SELECT * FROM A UNION SELECT * FROM B => A와 B 테이블의 전부를 하나의 데이터로 결합하여 출력한다.
```
##### INTERSECT
```
- A와 B 의 결과값의 교집합이라 생각하면된다. 
- SELECT employee_id FROM keys INTERSECT SELECT employee_id FROM hipos; => A와 B의 결과값중에서 리턴값이 똑같은 것만 출력한다.
```
##### EXCEPT 
```
- 첫번째 쿼리 결과셋들 중에서 두번째 쿼리 결과셋에 나오지않는 결과값들만 리턴한다. A - ANB
```
### Grouping Sets
- ##### GROUPING SETS 
	```
	- GROUP BY 절에서 그룹 조건을 여러개 지정할 수 있는 함수.
	- 각 그룹 조건을 별도로 GROUP BY 한거에 UNION ALL 한 결과와 동일하다.
	- 단순 CUBE 명령어 사용시 내가 원치 않는 모든 조합의 결과물을 보여주는데 이는 원하는 조합만 볼수 있다.
s
	- SELECT brand, segment SUM (quantity) FROM sales GROUP BY GROUPING SETS (brand, segment)m, (brand), (segment), ());
	```
- ##### CUBE 
```
	- SELECT c1,c2,c3 FROM table GROUP BY CUBE(c1,c2,c3) => select 한 열들의 모든 조합을 그룹핑해서 보여준다.
	- CUBE(c1,c2,c3) === GROUPING SETS ( (c1,c2,c3), (c1,c2), (c1,c3), (c2,c3), (c1), (c2), (c3), ())
```
- ##### ROLLUP
```
	- ROLLUP(c1,c2,c3) 의 결과물 GROUPING SETS ((c1,c2,c3), (c1,c2), (c1), ())
```

### Subquery
```
- IN(= ANY 랑 동일), ALL, EXIST, 부등호 등과 함께 좀더 복잡한 쿼리를 구성하는데 사용된다.
- 실행순서는 서브쿼리 -> 서브쿼리 결과를 본쿼리에 던져줌 -> 본쿼리를 실행
```
##### ANY
```
- ANY 뒤에 오는 결과는 오직 하나의 열데이터만 가능
- 무조건 =, <= , >. < <> 와 같이쓰여야됨.

```
##### ALL
```
- 서브쿼리 결과로 나오는 리스트 값들을 또다른 값과 비교할수 있게 한다.
- column_name comparison_operator ALL (subquery) 서브쿼리 결과로 나온 값들 모두가 colum_name 과 조건문을 만족해야 true를 리턴한다.
```
##### EXISTS
```
- EXISTS (subquery) 
- 서브쿼리가 최소한 하나의 row 만 리턴하여도 true를 리턴한다. 아무런 데이터가 없을시만 false
- SELECT first_nbame FROM customer c WHERE NOT EXISTS (SEKECT 1 FROM payment p WHAER p.customer_id = c.customer_id)
```
### Modifying data

### PostgreSQL import & export
### Managing tables
### PostgreSQL data types in depth
### Understanding PostgreSQL constraints
### Conditional expressions & operators
### PostgreSQL utilities
### PostgreSQL recipes