# 회원 관리 예제 - 웹 MVC 개발
---
### 회원 웹 기능 - 홈 화면 추가

- **홈 컨트롤러 추가**
    ```java
    @Controller
    public class HomeController {
    @GetMapping("/")
    public String home() {
        return "home";
    }
    }
    ```

- **회원 관리용 홈**

<br>

> **참고**: 컨트롤러가 정적 파일보다 우선 순위가 높다.

<br>

### 회원 웹 기능 - 등록

#### 회원 등록 폼 개발

- **회원 등록 폼 컨트롤러**
    ```java
    @Controller
    public class MemberController {
    ...

        @GetMapping(value = "/members/new")
        public String createForm() {
            return "members/createMemberForm";
        }
    }
    ```

- **회원 등록 폼 HTML**

<br>

#### 회원 등록 컨트롤러

- **웹 등록 화면에서 데이터를 전달 받을 폼 객체**

    ```java
    public class MemberForm{
        private String name;

        ...
    }
    ```

- **회원 컨트롤러에서 회원을 실제 등록하는 기능**

    ```java
    @PostMapping(value = "/members/new")
    public String create(MemberForm form){
        Member member = new Member();
        member.setName(form.getName());

        memberService.join(member);

        return "redirect:/";
    }
    ```

<br>

### 회원 웹 기능 - 조회

- **회원 컨트롤러에서 조회 기능**
    ```java
    @GetMapping(value = "/members")
    public String list(Model model) {
        List<Member> members = memberService.findMembers();
        model.addAttribute("members", members);
        return "members/memberList";
    }
    ```

- **회원 리스트 HTML**