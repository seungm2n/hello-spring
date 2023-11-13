# 회원 관리 - 백엔드 개발
- 비즈니스 요구사항 정리
- 회원 도메인과 레포지토리 만들기
- 회원 레포지토리 테스트 케이스 작성
- 회원 서비스 개발
- 회원 서비스 테스트

## 비즈니스 요구사항 정리
- 데이터 : 회원ID, 이름
- 기능 : 회원 등록, 조회
- 아직 데이터 저장소가 선정되지 않은 가상의 시나리오
  - 어떤 DB를 사용할지 선정 X
- 컨트롤러 : 웹 MVC의 컨트롤러 역할
- 서비스 : 핵심 비즈니스 로직 구현
- 레포지토리 : 데이터베이스에 접근, 도메인 객체를 DB에 저장하고 관리
- 도메인 : 비즈니스 도메인 객체
  - ex) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨.
- 아직 데이터 저장소가 선정되지 않아, 우선 인터페이스로 구현 클래스를 변경할 수 있도록 설계
- 데이터 저장소는 RDB, NoSQL 등등 다양한 저장소를 고민중인 상황
- 개발을 진행하기 위해 초기 개발 단계에서는 구현체로 가벼운 메모리 기반의 데이터 저장소 사용

## 회원 도메인과 레포지토리 만들기


## 회원 레포지토리 테스트 케이스 작성
- 개발한 기능을 실행해서 테스트 할 때 자바의 main 메서드를 통해서 실행하거나, 웹 애플리케이션의 컨트롤러를 통해서 해당 기능을 실행한다.  
- 이러한 방법은 준비하고 실행하는데 오래 걸리고, 반복 실행하기 어렵고 여러 테스트를 한번에 실행하기 어렵다는 단점이 있다.  
- 자바는 JUnit이라는 프레임워크로 테스트를 실행해서 이러한 문제를 해결할 수 있다.

### 회원 레포지토리 메모리 구현체 테스트
`src/test/java`하위 폴더에 생성한다.
```java
import com.example.hellospring.domain.Member;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;

import java.util.List;

import static org.assertj.core.api.AssertionsForClassTypes.assertThat;

class MemoryMemberRepositoryTest {

    MemoryMemberRepository repository = new MemoryMemberRepository();


    // 하나의 테스트가 끝날 때마다 지워주기 위함.
    @AfterEach
    public void afterEach() {
        repository.clearStore();
    }

    @Test
    public void save() {
        Member member = new Member();
        member.setName("spring");

        repository.save(member);

        Member result = repository.findById(member.getId()).get();
        // Assertions.assertEquals(member, result);
        assertThat(member).isEqualTo(result);
    }

    @Test
    public void findByName() {
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        repository.save(member2);

        Member result = repository.findByName("spring1").get();
        assertThat(result).isEqualTo(member1);
    }

    @Test
    public void findAll() {
        Member member1 = new Member();
        member1.setName("spring1");
        repository.save(member1);

        Member member2 = new Member();
        member2.setName("spring2");
        repository.save(member2);

        List<Member> result = repository.findAll();
        assertThat(result.size()).isEqualTo(2);
    }
}
```

## 스프링 빈과 의존관계

### 스프링 빈을 등록하고 의존관계 설정
- 회원 컨트롤러가 회원서비스와 회원 레포지토리를 사용할 수 있게 의존관계를 준비함.

### 회원 컨트롤러에 의존관계 추가
```java

```

#### 스프링 빈을 등록하는 두가지 방법
- 컴포넌트 스캔과 자동 의존관계 설정
- 자바 코드로 직접 스프링 빈 등록하기

#### 컴포넌트 스캔과 자동 의존관계 설정

- `@Component` 애노테이션이 있으면 스프링 빈으로 자동 등록
- `@Controller` 컨트롤러가 스프링 빈으로 자동으로 등록되는 이유도 컴포넌트 스캔 때문

- `@Component`를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록
  - `@Controller`
  - `@Service`
  - `@Repository`

