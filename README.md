# Database 
##### ( 블로그를 따라치면서 정리 : https://yaboong.github.io/database/2018/03/09/database-anomaly-and-functional-dependency/ )
- SQL문 : 대소문자 구별하지 않음 (단, 데이터의 대소문자는 구분)

- SQL 구문은 DCL , DDL , DML 로 구분될 수 있다. 

### DDL  ( 데이터 정의어 )

- 데이터베이스 객체의 구조를 정의한다. 

- 테이블 생성, 컬럼 추가, 타입변경, 제약조건 지정, 수정 등

  - CREATE : 데이터베이스 객체를 생성
  - DROP : 데이터베이스 객체를 삭제 
  - ALTER :  기존에 존재하는 데이터베이스 객체를 수정

  

  CREATE DATABASE SSAFYDB;

  CREATE DATABASE SSAFYWEB 

  DEFAULT CHARACTER SET UTF8MB4

  COLLATE UTF8MB4_GENERAL_CI;   

​       

​       CREATE TABLE PRODUCT (

​        PRODUCTNO INT PRIMARY KEY AUTO INCREMENT, 

​         NAME VARCHAR(30) NOT NULL,

​        PRICE INT DEFAULT 0, 

​        REGISTERDATE TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP 

​        ) ENGINE = InnoDB DEFAULT CHARSET = utf8;

- Optional Attrivutes 및 제약 조건 

  - **테이블** **생성** **제약조건**

  - **총 5가지** 

    - NOT NULL : NULL값 포함할 수 없음 , 반드시 쿼리문을 이용하여 값을 지정 

    - 유니크 :  컬럼에 중복된 값을 저장할 수 없음. NULL값은 허용 

    - PRIMARY KEY :  컬럼에 중복된 값을 저장할 수 없음 .NULL값도 허용하지 않음 

      ​                              주로 ROW를 구분하기 위한 유일한 값을 지정할 때 사용 ' 기본키'

    - FOREINGN KEY : 특정 테이블의 PK컬럼에 저장되어 있는 값만 저장 '참조값' ,'외래키'라고도 부름 . NULL값은 허용 . references를 이용하여 어떤 컬럼에 어떤 데이터를 참조하는지 반드시  지정 

    - DEFAULT 'value' : NULL 값이 들어올 경우 기본 설정되는 값을 지정 

    - CHECK : 해당 칼럼에 저장 가능한 데이터 값의 범위나 조건을 지정한다. 

  ​          

  +  UNSINGED : Type이 숫자인 경우만 해당되며 숫자가 0 또는 양수로 제한됨 
  +  AUTO INCREMENT : 새 레코드가 추가 될 때마다 필드 값을 자동으로 1증가시킴 

- DROP : 객체 삭제 

  ` DROP DATABASE SSAFYWEB;`

- ALTER : 기존에 존재하는 객체 수정 

  `ALTER DATABASE SSAFYDB`

  `DEFAULT CHARACTER SET UF816 ...`

 ### DML (데이터조작어)

- 데이터 조작 기능

- 테이블의 레코드를 CRUD (Create, Retrieve, Update , Delete) 할 수 있다. 

- insert(c)  : 데이터베이스 객체에 데이터를 입력

- select(r) : 데이터베이스 객체에서 데이터를 조회

- update(u) : 데이터베이스 객체에 데이터를 수정

- delete(d) : 데이터베이스 객체에 데이터를 삭제

  `INSERT INTO PRODUCT` 

  `VALUES ( 1, "PRODUCT1" , 5000, NULL);`

   `INSERT INTO PRODUCT (NAME, PRICE)`

  `VALUES ("PRODUCT2". 10000);`

  ====================================================

  `UPDATE PRODUCT` 

  `SET NAME="NEWNAME"`

  `WHERE PRODUCTNO = 1;  // 주의 WHERE절을 생략하면 모든 데이터가 바뀜` 

  =======================================================

  `DELECT FROM PRODUCT`

  `WHERE NAME = "NEWNAME" ; // 주의 WHERE절을 생략하면 모든 데이터가 바뀜` 

  ==============================================================

  `SELECT *`

  `FROM PRODUCT;` 

  ==============================================================

  `SELECT PRODUCTNO,  PRICE`

  ​     `CASE WHEN PRICE >  50000 THEN '고가'` 

  ​                `ELSE  '저가'`

  ​     `END '가격 분류'`

  `FROM PRODUCT;` 

  ================================================================

  `SELECT PRODUCTNO, NAME`

  `FROM PRODUCT` 

  `WHERE PRICE < 40000;`

  `` 

  `SELECT PRODUCTNO , NAME`

  `FROM PRODUCT` 

  `WHERE NAME LIKE "%TV%"`

  `OR NAME LIKE "%PHONE%" ;` 

``        

​        `SELECT PRODUCTNO , NAME`

​         `FROM  PRODUCT`

​       `WHERE NOT PRODUCTNO = 1;` 

================================================================

​        `SELECT PRODUCTNO , NAME`

`FROM PRODUCT` 

`WHERE PRICFE = NULL;` 

`SELECT PRODUCT NO, NAMKE`

`FROM PRODUCT` 

`WHERE PRICE IS NULL;` 

`SELECT PRODUCT NO, NAMKE`

`FROM PRODUCT` 

`WHERE PRICE IS NOT NULL;` 

==================================================

### DCL (데이터 제어어)

- DB, Table의 접근권한이나 CRUD 권한을 정의
- 특정 사용자에게 테이블의 검색권한 부여 / 금지 등 
- grant : 데이터베이스 객체에 권한을 부여
- revoke : 데이터베이스 객체 권한을 취소한다. 

### TCL  ( 트랜잭션 제어어 )

- transaction 란 데이터베이스의 논리적 연산 단위 
  - commit : 실행한 Query를 최종적으로 적용
  - rollback : 실행한 Query를 마지막 commit 전으로 취소시켜 데이터를 복구 

### 간단 자료형

date : yyyy - mm- dd

time : hh:mm:ss

datetime : yyyy-mm-dd hh:mm:ss

timestamp: 1970-01-01 ~ 2037년 임의시간 

- CHAR <-> VARCHAR 

​          -  CHAR(20) : 20 공간 만큼 FILE SYSTEM에 할당

- VARCHAR(20) : 저장한 크기만큼 할당됨 
  - 길이가 20인 단어로 수정하게 된다면? 빈공간에 저장, LINK로 저장공간을 연결 

**이진 데이터타입**  

   - BINARY[(숫자)] -> 문자열로 저장됨 

     

     ### 내장함수

     - ABS(절댓값), ROUND, TRUNCATE, POW, MOD (분자,분모)

     - ROUND(숫자, 자릿수) :  자릿수 기준 반올림 -> '자릿수'까지 표현하겠다 
     - ASCII(문자) : 아스키값 리턴 
     - INSTR('문자열', '찾는문자열' ) : 위치 값 리턴 
     - LEFR, RIGHT('문자열' ,개수)  
     - REVERSE ('문자열') : 반전 
     - LTRIM ('문자열') : 문자열 중 왼쪽의 공백을 제거 
     - TRIM('문자열') : 양쪽 모두의 공백을 제거 

     - LOWER('문자열') : 모든 문자를 소문자로 변경 
     - UPPER('문자열') : 모든 문자를 대문자로 변경 

     - YEAR , MONTH, MONTHNAME, DAYNAME (날짜) 
     - DAYOFWEEK(날짜) : 일 1 ~ 토 7 
     - WEEKDAY(날짜) : 월 0 ~ 일 6

  #### 트랜잭션 명령어 

      - ROLLBACK : 트랜잭션 선언 전으로 돌아감
      - COMMIT  : 트랜잭션 이후 모든 동작을 적용 
      - SAVEPOINT  POINT 1 : 세이브포인트를 지정 
      - ROLLBACK TO SAVEPOINT POINT 1 : POINT 1 이전으로 돌아감 



### VIEW 

- 복잡한 쿼리문의 단순화를 위한 '가상테이블'

- 물리적으로 저장되지 않음 

- 목적

  - 보안 - 일부 column만 view를 통해 접근하도록 
  - 사용상의 편의 - view 생성을 통해 복잡한 쿼리의 단순화 
  - 수행속도의 향상 

  `create view 뷰이름` 

  `as` 

  `select 문` 

  `예시` 

  `create or replace view employee`

  `as` 

  `select empno, ename , job , hiredate, sal` 

  `from emp`

  `lest join dept`

  `using(deptno)`

### INDEX

- 지정한 컬럼을 기준으로 메모리 영역에 목차를 Btree 형태로 생성 
- 목적 : 데이터 조회의 성능 향상
- PK & FK 에 대해 자동 인덱스를 생성함 

​         `CREATE INDEX 인덱스명  ON 테이블명(컬럼명, ... );` 

​         `CREATE INDEX idx_emp_ename on emp(ename);` 

​         

### JDBC

- Java application이 RDB에 접속하기 위한 Java Standard API 
- JDBC 프로그램이 순서 4단계 
- ![image-20201021071001025](C:\Users\eunseon\AppData\Roaming\Typora\typora-user-images\image-20201021071001025.png)

1. JDBC 드라이버 로딩 

   public class DBUtil {

    static  String url = "jdbc:mysql:// localhost:3306/ssafy_hrm?server?~"

    static  String user = "ssafy";

   static String pw = "ssafy"; 

   static (

   1. jdbc드라이버 로딩 

      //Class.forName 메소드를 이요해 드라이버 로딩 

      try {

      Class.forName("com.mysql.cj.jdbc.Driver");

      }catch (Exception e){

       e.printStackTrace();

        sout("drive loading 실패");

      }

      )

   }

2. 데이터베이스와 연결 

3. SQL 문 실행 

   3-1 . statement/ preparedstatement 객체를 사용해 원하는 SQL 문 실행

   3-2 . ResultSet에서 데이터 추출 

4. 데이터베이스와의 연결 끊기 (자원반납)

   //2. 데이터베이스와 연결 

   conn = DBUtil.getConncetion ();

   StringBuilder sql = new StringBuilder();

   // 3. sql 문 실행 

   sql.append("select ~"); 

   //3-1. statment객체 생성하여 sql문 실행 

   // connection 객체로 접근해 prepareStatement()메소드를 호출해 생성 

   pstmt = conn.prepareStatement(sql.toString());

   pstmt.setInt(1,productno); 

   //3-2. SQL문 실행해 결과를 rs에 저장

   select 문 -> excuteQuery(); 

   update, delete, insert문 -> executeUpdate(); 

   rs= pstmt.executeQuery (); 

   //ResultSet에서 데이터 추출

   if(rs.next()){

   productDto= new Product();

   productDto.setProductno(rs.getnt("productno"));

   productDto.setName(rs.getnt("productno"));

   productDto.setPrice(rs.getnt("productno"));

   

   }

   //4. 자원반납 

   DButil.close(rs);

   
### SQL 정리 

#### 정규화가 필요한 이유 

- 데이터베이스를 잘못 설계하면 불필요한 데이터 중복으로 인한 공간낭비를 넘어 부작용을 초래 할 수 있다. 이러한 부작용을 이상이라고 하는데 이상이라고 하는데 이상현상의 종류로 삽입이상, 갱신이상,삭제이상이 있다. 

- 학사정보시스템을 예제로한 데이터베이스 설계에서 잘못된 테이블 설계로 인해 나타날 수 있는 이상현상에 대해 살펴보자

- 아래 예제에서 한 튜플을 고유하게 식별할 수 있는 속성의 조합은 학번과 과목코드이고 이를 의미하는 STUDENT_ID , COURSE_ID의 조합을 기본키로 가지는 테이블이다. 한 학생은 하나의 DEPARTMENT(학부)에만 속할 수 있다고 가정하자 

  ![image-20201015233823225](C:\Users\eunseon\AppData\Roaming\Typora\typora-user-images\image-20201015233823225.png)

#### 삽입이상 

아직 수업을 하나도 수강하지 않은 학생이 있다고 가정하자. 현재 KEY를 학번과 과목코드로 지정해놓았고 기본키로 쓰이는 컬럼은 NULL이 될 수 없으므로 그 학생은 이 테이블에 추가 될 수 가 없다. 굳이 삽입하려면 '미수강' 같은 과목코드를 새로 만들어서 삽입해야한다. 

- 새 데이터를 삽입하기 위해 불필요한 데이터도 함께 삽입해야 하는 문제를 삽입이상이라고 한다. 

  

#### 갱신이상

야봉이 컴공이 싫어서 음악학부로 옮기게 되는 경우 '컴공'의 갯수는 과목코드의 갯수 만큼 있으므로 모두 '음악학부'로 변경해 줘야한다. 이때 모두 변경하지 않고 두개만 바꾸는 경우 야붕은 컴공인지 음악학부인지 알 수 없게 된다. 

- 중복 튜플 중 일부만 변경하여 데이터가 불일치하게 되는 모순의 문제를 갱신이상이라고 한다. 



#### 삭제이상 

- 위 테이블에서 모찌는 현재 1개의 과목만 수강하고 있다. 모찌가 수강정정기간에 과목이라는 수업을 듣기 싫어져서 드랍하는 경우, 위 테이블에 반영하기 위해서는 모찌에 대한 행을 모두 삭제하게 된다. 수강취소를 반영하기 위해 학생등복정보를 모두 날리게 되는 것이다 

  ->  튜블을 삭제하면 꼭 필요한 데이터까지 함께 삭제되는 데이터 손실의 문제를 삭제이상이라고 한다. 



위와 같은 이상현상이 발생하는 이유는 정규화가 되어 있지 않은 테이블 설계 때문이다. 코딩할때에도 관심사를 분리하면 코드의 재사용성과 유지보수의 편의성이 높아지는 것처럼 데이터베이스 설계에서도 비슷한 원칙이 적용된다. 데이터베이스 설계의 경우 관심사를 분리하지 않아 생기는 문제는 코드단에서의 문제보다 훨씬 치명적이다. 

이론적으로는 정규화를 수행하려면 속성들간의 관련성을 파악해야 하는데, 이 속성들간의 관련성을 함수적 종속성라고 한다. 일반적을로 하나의 릴레이션에는 하나의 함수적 종속성만이 존재하도록 정규화를 하게 된다. 

#### 함수적 종속성 

- 함수적 종속성은 아래와 같이 표현할 수 있다. 

  X -> Y 

  - X는 결정자.  Y는 종속자라고 한다. 

  - X가 Y를 함수적으로 결정한다. 

  - Y가 X에 함수적으로 종속되어 있다. 

    ![image-20201015235249716](C:\Users\eunseon\AppData\Roaming\Typora\typora-user-images\image-20201015235249716.png)

- 위와 같은 학생 릴레이션을 대상으로 속성 간 함수적 종속성에 대해 알아보자 
- 학번에 의해서 학생이름과 학부는 고유하게 구분되므로 학생이름 , 학부 속성은 학번에 함수적으로 종속되어 있다고 할 수 있다. 여기서 학번은 결정자, 학생이름과 학부는 종속자가 되며 함수적 종속성은 아래와 같은 기호로 표현할 수 있다. 
- 학번 -> (학생이름, 학부 )
- 주의할 점은 현 시점의 속성 값만으로 판단하면 안된다. 속성 값은 계속 변할 수 있는 것이기 때문에 속성 자체가 가지는 특성과 의미를 기반으로 판단해야 한다. 



##### 부분 함수적 종속 

- 속성집합 Y가 속성집합 X의 전체가 아닌 일부분에도 함수적으로 종속됨을 의미한다. 
- 이름이 속성집합 Y이고, {학번, 과목코드} 가 속성집합 X인 상태에서 이름은 {학번, 과목코드}에도 함수적으로 종속되며 X의 일부인 학번에도 한수적으로 종속된다. 

##### 완전 함수적 종속 

- 속성집합 Y 가 속성집합X전체에 대해서만 함수적으로 종속된 경우를 말한다. 

- 성적이 속성집합 Y이고, {학번, 과목코드} 가 속성집합 X인 상태에서 , 성적은 {학번, 과목코드}의 어떤 부분집합에도 함수적으로 종속되어있지 않다. 학번만으로 성적을 결정지을 수 없고 , 과목코드만으로도 성적을 결정지을 수 없기 때문이다. 

- 일반적으로 함수적 종속성을 말하면 완전함수종속을 의미한다. 

  

 #### 정규화

- 관계형 데이터베이스의 설계에서 중복을 최소화하게 데이터를 구조화하는 프로세스를 정규화 라고 한다. 

- 조금 더 이론적으로 접근해 보면 함수적 종속성을 이용해서 연관성 있는 속성들을 분휴하고, 각 릴레이션들에서 이상현상이 생기지 않도록 하는 과정을 말한다. 

- 정규화 된 정도를 정규형으로 표현하는데,  정규형에는 1NF,2NF,3NF,BCNF,4NF,5NF,6NF까지 있다. 

  비공식적인 표현으로는 3NF  가 되었으면 정규화되었다고 말한다. 

- 각 정규형이 되기 위해서는 만족시켜야 할 제약조건들이 있다. 높은 차수의 정규형으로 갈 수록 조건이 까다롭다. 



#### 제 1 정규형 

- 제1정규형에 대한 정의는 릴레이션에 속한 모든 속성의 도메인이 원자 값으로만 구성되어 있으면 제 1정규형에 속함. 
- 관계형 데이터베이스의 릴레이션은 모든 속성이 원자 값이 가지는 특성이 있기 때문에, 최소한 제 1정규형을 만족해야 릴레이션이 될 자격이 있다. 



#### 제 2 정규형

- 제1정규형만 만족시키는 릴레이션에서 부분 함수 종속성을 가지게 되는 경우 삽입이상, 갱신이상, 삭제이상 세가지 이상현상이 모두 나타나게 된다. 

- 제 1정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속되면 제2정규형이다. 

- 제 2정규화를 수행 했을때 결과적으로 모든 컬럼이 완전 함수적 종속을 만졳한다. (부분 함수적 종속을  모두 제거되었다.) 이를 이해하기 위해 부분 함수적 종속과 완전 함수적 종속이라는 용어를 알아야 한다.  

- {학번, 과목코드} -> 성적

  {학번, 과목코드} -> 학부 

  {학번, 과목코드} -> 등록금

  학번 -> 학부 

  학번 -> 등록금 

  학부 -> 등록금 

  - 현재 학번 -> 학부, 학번 -> 등록금 두개의 부분 함수 종속성을 가지고 있다. 
  - ![image-20201015230800822](C:\Users\eunseon\AppData\Roaming\Typora\typora-user-images\image-20201015230800822.png)

- 현재 학번 -> 학부 , 학번 -> 등록금 두개의 부분  함수 종속성을 가지고 있다. 이를 제거해주는 것을 제 2정규화 라고 한다. 
- 학번, 학부, 등록금 속성을 자기는 학생 릴레이션과  학번, 과목코드 , 성적 속성을 가지는 성적릴레이션들로 나누어 주면 부분 함수 종속성을 제거할 수 있다. 
- 학버 -> 학부 함수종속성으로 볼때, 학번만으로 학부에 대한 결정을 지을 수 있다는 말이다. 그러나 현재 기본키가 학번, 과목코드로 이루어져 있기 때문에 학번만으로 학부에 대한 결정을 지을 수 있다는 게 의미가 없어진다. 그래서 이를 가능하도록 해주는 과정이 부분 함수 종속성을 제거하는 제 2정규화 과정이다. 

- 여기서 학부 -> 등록금 이라는 함수적 종속성은 부분 함수 종속성이 아니다. X -> Y 라는 함수적 종속성에서 부분 함수 종속성, 완전 함수 종속성을 따질때 결정자 X가 반드시 기본키나 후보키에 속할 필요는 없으므로 현재 학부 -> 등록금 의 함수 종속은 하나의 완전 함수 종속이라고 볼 수 있다. 

- 릴레이션이 둘로 분해되면서 학부와 등록금에 대한 중복항목이 제거되었다. 정규화 과정에서 주의할 점은 정규화를 통해 분해된 릴레이션들이 조인을 통해 원래의 구조로 복원될 수 있어야 한다는 것이다. 

- 두 릴레이션 모두 제 1 정규형에 속하고, 기본키가 아닌 모든 속성이 기본키에 완전 함수 종속되므도 제 2정규형을 만족한다. 

  - 제 2 정규형을 만족하면 이상현상이 없어질까?

    -> 그렇지 않다. 

  - 삽입이상 

    -> 새로운 학부가 생기는 경우 등록된 학생 (학번)이 없다면 학번 속성이 NULL이 되므로 삽입할 수 없다. 

  - 갱신이상

    -> 컴퓨터공학부 등록금이 400으로 오르는 경우 20800399 , 21500399 둘 모두 바꾸어 주지 않음녀 데이터 불일치 문제가 발생한다. 

  - 삭제이상 

    -> 21400001 학번을 가진 학생이 자퇴하는 경우, 기계공학부에 대한 정보가 함께 사라진다. 

  - 제 2정규형에서도 이상현상이 발생하는 이유는 이행적 함수 종속이 존재하기 때문이다. 이행적 함수 종속을 없애주는 과정이 제 3 정규화이다. 

  

#### 제 3 정규형

- 제 2정규형에 속하면서, 기본키가 아닌 모든 속성이 기본키에 이행적 함수 종속이 되지 않으면 제 3 정규형이다. 

  

##### 이행적 함수 종속 

-  삼단논법 같은 관계를 가진 함수종속이다.  X,Y,Z 에 대해 X -> Y , Y -> Z,  X->Z 가 성립한다. 이를 Z가 X에 이행적으로 함수 종속되었다고 한다. 

- 지금 학생 릴레이션에서 함수적 종속성은 아래와 같다. 

  학번 -> 학부 

  학부 -> 등록금 

  학번 -> 등록금 

  논리적으로 말은 되는데 의미상 뭔가 이상하다. 학부에 따라 등록금이 결정되는 것이지 학번에 따라 결정되는 것은 아니다. 그냥 이걸 둘로 분리 해주면 된다. 

  X -> Y, Y-> Z 함수적 종속관계로 인해 X -> Z 의 이행적 함수 종속 관계가 나타나면 [X,Y] .[Y,Z] 두 릴레이션으로 분해된다. 

  분리하여 이행적 종속 관계를 제거 한 학생 릴레이션과 학부 릴레이션은 아래와 같다. 

![image-20201015232619672](C:\Users\eunseon\AppData\Roaming\Typora\typora-user-images\image-20201015232619672.png)

- 제 3 정규형을 만족하면 이상현상이 없어질까?

  - 그렇지 않다. 지금까지 살펴본 세가지 릴레이션에서는 기본키가 될 수 있는 후보키가 하나 밖에 없었다. 하지만 후보키를 여러개 가지고 있는 릴레이션에서는 제3정규형을 만족하더라도 이상현상이 생길 수 있다. 

    이를 해결하기 위한 정규형이 보이스-코드 정규형(BCNF ) 이다. 제 3 정규형보다 조금 더 엄격한 제약조건을 가지기 때문에 Strong 3NF 라고도 한다. 

    

