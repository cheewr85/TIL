![one](/img/Spring/AOP/one.png)

```java
package hello.helloworld.service;

import hello.helloworld.domain.Member;
import hello.helloworld.repository.MemberRepository;
import hello.helloworld.repository.MemoryMemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;
import java.util.Optional;

@Transactional
public class MemberService {

    // 서비스 위해 리포지토리 필요함
    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    // 회원가입 기능
    public Long join(Member member) {
//        // 같은 이름이 있는 중복회원은 안됨
////        Optional<Member> result = memberRepository.findByName(member.getName());
////        // 만일 값이 이미 존재한다면, Optional을 쓰기 때문에 아래와 같이 확인해서 쓸 수 있음
////        result.ifPresent(m -> {
////            throw new IllegalStateException("이미 존재하는 회원입니다.");
////        });
//        // 위의 주석처리 부분은 깔끔하지는 못함, 어차피 Optional을 반환하기 때문에 아래와 같이 쓸 수 있음, 하지만 이런건 메소드로 빼는게 좋음, 메소드로 뺌
////        memberRepository.findByName(member.getName())
////                .ifPresent(m -> {
////                    throw new IllegalStateException("이미 존재하는 회원입니다.");
////                });

        long start = System.currentTimeMillis();

        try {
            // 중복회원 검증, ExtractMethod로 뺌
            validateDuplicateMember(member);
            // 그냥 해당 멤버를 세이브해서 아이디 넘겨줌
            memberRepository.save(member);
            return member.getId();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("join = " + timeMs + "ms");
        }
    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    // 전체 회원 조회
    public List<Member> findMembers() {
        long start = System.currentTimeMillis();
        try {
            return memberRepository.findAll();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("findMembers = " + timeMs + "ms");
        }
    }

    // 회원 조회
    public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
    }
}
```

- 하지만 아래와 같은 문제가 생김
- 이 부분을 단순히 2~3개가 아니라 1000천개라고 하면 매우 오래걸리고 비효율적이게 됨

![one](/img/Spring/AOP/two.png)

### AOP 적용
- AOP : Aspect Oriented Programming
- 공통관심사항과 핵심관심사항을 분리하는 것임

![one](/img/Spring/AOP/three.png)

- 이를 AOP를 통해서 적용하고 지정해서 관리할 수 있음
- 먼저 별도로 패키지를 만들고 파일을 만듬, 아까 처리한 타임 체크에 대한 로직을 만들어둠
- 그리고 Configuration 해서 Spring BEAN에 직접 등록을 하는 방법도 있고 위처럼 Component 애너테이션을 활용해서 스캔할 수 있음
- 그리고 Around를 통해서 위에서 사진에서 보인것처럼 공통사항 적용을 타켓팅 할 수 있음
- 아래처럼 패키지 하위 다 적용하는 것외에 타켓팅해서 특정 클래스 등등에 직접 설정가능함

```java
package hello.helloworld.aop;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class TimeTraceAop {

    @Around("execution(* hello.hellospring..*(..))") // 패키지 하위에 다 적용함
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());
        try {
            // 다음 포인트로 진행가능
            return joinPoint.proceed();
        } finally {
            long finish = System.currentTimeMillis();
            long timeMs = finish - start;
            System.out.println("END: " + joinPoint.toString() + " " + timeMs + "ms");
        }
    }
}
```

- 그러면 이제 시간측정 로직에 대해서 아래와 같이 Serviec에서 다 빼고 핵심 로직만 남길 수 있음

```java
package hello.helloworld.service;

import hello.helloworld.domain.Member;
import hello.helloworld.repository.MemberRepository;
import hello.helloworld.repository.MemoryMemberRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

import java.util.List;
import java.util.Optional;

@Transactional
public class MemberService {

    // 서비스 위해 리포지토리 필요함
    private final MemberRepository memberRepository;

    public MemberService(MemberRepository memberRepository) {
        this.memberRepository = memberRepository;
    }

    // 회원가입 기능
    public Long join(Member member) {
//        // 같은 이름이 있는 중복회원은 안됨
////        Optional<Member> result = memberRepository.findByName(member.getName());
////        // 만일 값이 이미 존재한다면, Optional을 쓰기 때문에 아래와 같이 확인해서 쓸 수 있음
////        result.ifPresent(m -> {
////            throw new IllegalStateException("이미 존재하는 회원입니다.");
////        });
//        // 위의 주석처리 부분은 깔끔하지는 못함, 어차피 Optional을 반환하기 때문에 아래와 같이 쓸 수 있음, 하지만 이런건 메소드로 빼는게 좋음, 메소드로 뺌
////        memberRepository.findByName(member.getName())
////                .ifPresent(m -> {
////                    throw new IllegalStateException("이미 존재하는 회원입니다.");
////                });

        // 중복회원 검증, ExtractMethod로 뺌
        validateDuplicateMember(member);
        // 그냥 해당 멤버를 세이브해서 아이디 넘겨줌
        memberRepository.save(member);
        return member.getId();

    }

    private void validateDuplicateMember(Member member) {
        memberRepository.findByName(member.getName())
                .ifPresent(m -> {
                    throw new IllegalStateException("이미 존재하는 회원입니다.");
                });
    }

    // 전체 회원 조회
    public List<Member> findMembers() {

        return memberRepository.findAll();

    }

    // 회원 조회
    public Optional<Member> findOne(Long memberId) {
        return memberRepository.findById(memberId);
    }
}
```

- 다양한 조건들을 AOP에 설정해서 적용할 수 있음

![one](/img/Spring/AOP/four.png)

- AOP 적용하기 전에는 아래와 같이 Controller에서 Service를 호출하는 구조였음, 의존관계를 활용해서

![one](/img/Spring/AOP/five.png)

- AOP를 적용하고 타켓팅을 하면 서비스가 딱 지정이 됨, 그렇게 된다면 가짜 프록시 Service를 만들어서 앞에 세워둠, 이 프록시 Service가 끝나면 그 이후 실제 Service에 연결함 그때 실행이 됨
- 즉 가짜 멤버 Service를 불러옴 Controller에서

![one](/img/Spring/AOP/six.png)

- 아래와 같이 전체 그림을 보면 아래와 같이 적용이 됨

![one](/img/Spring/AOP/seven.png)

- DI를 하기 때문에 이러한 AOP가 가능한 것임