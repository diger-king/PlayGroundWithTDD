# 단위테스트란?

## main method의 용도

프로그램을 시작

구현한 프로그램을 테스트


## 사칙연산 계산기

### Production Code

    public class Calculator {
    
        int add(int i, int j) {
            return i + j;
        }    
    
        int substract(int i, int j) {
            return i - j;
        }

        int multiply(int i, int j) {
            return i * j;
        }
        
        int divide(int i, int j) {
            return i / j;
        }

### Test Code

    public static void main(String[] args) {
        Calculator cal = new Calculator();

        System.out.println(cal.add(3, 4));
        System.out.println(cal.substarct(5, 4));
        System.out.println(cal.multiply(2, 6));
        System.out.println(cal.divide(8, 4))
    }

**프로덕션 코드**는 프로그램 구현을 담당하는 부분으로, 사용자가 실제로 사용하는 코드를 의미한다.

**테스트 코드**는 프로덕션 코드가 정상적으로 동작하는지 확인하는 코드이다.

---

### Main Method 에 테스트 코드를 삽입했을 때의 문제점

**Production Code 와 Test Code 가 클래스 하나에 존재한다. --> 클래스 크기가 커지고, 복잡도가 증가한다.**

**Test Code 가 실 서비스에 같이 배포된다.**

**Main Method 하나에서, 여러 개의 기능을 테스트한다. --> 복잡도가 증가한다.**

**Method 이름을 통해 어떤 부분을 테스트하는지 의도를 드러내기 어렵다.**

**테스트 결과를 사람이 수동으로 확인해야한다. --> 엣지케이스를 놓치는 경우가 있을 수 있다.**

---

### 위 문제점을 해결하기 위한 도구 - JUnit

**Annotation 을 활용한 테스트 코드 구현 가능**

**@Test**

**@BeforeEach, @AfterEach**

**Assertions 클래스의, static assert method 를 활용해 테스트 결과 검증가능**

    import org.junit.jupiter.api.AfterEach;
    import org.junit.jupiter.api.BeforeEach;
    import org.junit.jupiter.api.Test;
    
    import static org.junit.jupiter.api.Assertions.assertEquals;
    
    public class CalculatorTest {
    Calculator cal;
    
        @BeforeEach
        public void setUp()  {
            cal = new Calculator();
        }
    
        @Test
        public void 덧셈()  {
            assertEquals(7, cal.add(3, 4));
        }
    
        @Test
        public void 뺄셈()  {
            assertEquals(1, cal.subtract(5,  4));
        }
    
        @Test
        public void 곱셈()  {
            assertEquals(6, cal.multiply(2, 3));
        }
    
        @Test
        public void 나눗셈()  {
            assertEquals(2, cal.divide(8, 4));
        }
    
        @AfterEach
        public void tearDown() {
            cal = null;
        }
    }