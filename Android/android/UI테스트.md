- 먼저 테스트를 위한 기기를 준비하거나 애뮬레이터를 통해서 테스트 할 수 있음
- Espresso에 대한 라이브러리를 추가하고 세팅을 해 둠
- 패키지에서 androidTest라고 되어 있는 부분에서 UI 테스트 가능함, test를 실행시키면 연결된 기기 혹은 애뮬레이터가 실행됙고 성공적으로 테스트가 완료되면 Tests passed 문구와 끝남
- 가장 먼저 해볼 테스트는 Send 버튼을 누르면 텍스트가 넘어가고 텍스트가 보이는 간단한 구조인데 이를 테스트 코드로 작성하여 UI가 정상적으로 작동하는지 확인함

```java
package techtown.org.twoactivity;

import android.content.Context;

import androidx.test.platform.app.InstrumentationRegistry;
import androidx.test.ext.junit.runners.AndroidJUnit4;
import androidx.test.rule.ActivityTestRule;

import org.junit.Rule;
import org.junit.Test;
import org.junit.runner.RunWith;

import static androidx.test.espresso.Espresso.onView;
import static androidx.test.espresso.action.ViewActions.click;
import static androidx.test.espresso.assertion.ViewAssertions.matches;
import static androidx.test.espresso.matcher.ViewMatchers.isDisplayed;
import static androidx.test.espresso.matcher.ViewMatchers.withId;
import static org.junit.Assert.*;

/**
 * Instrumented test, which will execute on an Android device.
 *
 * @see <a href="http://d.android.com/tools/testing">Testing documentation</a>
 */
@RunWith(AndroidJUnit4.class)
public class ActivityInputOutputTest {

    // 사용하기 위해서 라이브러리 추가했어야 함, androidx.test.rules
    @Rule
    public ActivityTestRule mActivityRule = new ActivityTestRule<>(MainActivity.class);

    @Test
    public void useAppContext() {
        // Context of the app under test.
        Context appContext = InstrumentationRegistry.getInstrumentation().getTargetContext();
        assertEquals("techtown.org.twoactivity", appContext.getPackageName());
    }

    // Send 버튼을 눌렀을 때 만약 Text가 없다면 SecondActivity가 나올지에 대한 테스트
    @Test
    public void activityLaunch() {
        // onView 메소드 Activity에서 테스트하려는 UI 구성 요소를 찾음(send 버튼)
        // 그런 다음 perform 즉, 메소드 호출 후 사용자 작업을 전달하여 해당 UI에서 실행할 특정 상호작용을 시뮬레이션 함, 여기선 click
        onView(withId(R.id.button_main)).perform(click());
        // 그런 다음 Send 버튼 눌렀을 때 Text 확인하기 위해 그 값을 불러옴
        // 그런 다음 matches에서 ViewAssertions 메서드를 통해서 예상 상태나 동작이 반영됐는지 확인, 제대로 Text가 노출되었는지
        onView(withId(R.id.text_header)).check(matches(isDisplayed()));
        // 이와 같이 Second 역시 확인함
        onView(withId(R.id.button_second)).perform(click());
        onView(withId(R.id.text_header_reply)).check(matches(isDisplayed()));
    }
}
```

- 위와 같이 코드를 설계하고 시작하면 자동으로 앱을 실행시키고 버튼을 누르고 View를 확인함 그리고 텍스트가 정상적으로 뜬다면 TestPassed가 되어 통과됨
- 그 다음 Edit Text에 테스트할 문장을 두고 입력한 뒤 버튼을 누르면 제대로 값이 넘어가서 매칭이 되는지 확인함

```java
// EditText에 입력하고 send를 했을 때 정상적으로 send 처리가 됐는지에 대한 테스트
    @Test
    public void textInputOutput() {
        onView(withId(R.id.editText_main)).perform(typeText("This is a test."));
        onView(withId(R.id.button_main)).perform(click());
        onView(withId(R.id.text_message)).check(matches(withText("This is a test.")));
    }
```

- 자동으로 입력하고 버튼을 누른뒤 처리함 똑같은 텍스트라면 passed 됨
- 여기서 만약 check하는 값이 다르게 처리했다면 실패하고 나오지 않음 아래와 같이

```java
// EditText에 입력하고 send를 했을 때 정상적으로 send 처리가 됐는지에 대한 테스트
    @Test
    public void textInputOutput() {
        onView(withId(R.id.editText_main)).perform(typeText("This is a test."));
        onView(withId(R.id.button_main)).perform(click());
        onView(withId(R.id.text_message)).check(matches(withText("This is a failing test.")));
    }
```

- 이를 통해서 미리 예상값과 입력값을 비교하면서 테스트를 할 수 있음
- 이외에 추가적으로 spinner의 아이템 값을 가져와서 선택해서 가져와서 보여지는 값이 맞는지 확인할 수 있음
- 그리고 이러한 Test에 대해서 Record를 하여 코드 형태로 보여줄 수도 있음
- 우선 아래와 같이 UI Test에 대한 Record를 할 수 있음

![one](/img/Android/android/UITest/one.png)

- 그리고 OK를 누른다면 이에 대한 Test를 이해하기 위한 Test 클래스 파일을 만들 수 있음, 자동으로 라이브러리를 추가하는 작업이 끝나고 아래와 같이 테스트 파일 코드가 완성됨

```java
package techtown.org.scorekeeper;

import android.view.View;
import android.view.ViewGroup;
import android.view.ViewParent;

import androidx.test.espresso.ViewInteraction;
import androidx.test.filters.LargeTest;
import androidx.test.rule.ActivityTestRule;
import androidx.test.runner.AndroidJUnit4;

import org.hamcrest.Description;
import org.hamcrest.Matcher;
import org.hamcrest.TypeSafeMatcher;
import org.hamcrest.core.IsInstanceOf;
import org.junit.Rule;
import org.junit.Test;
import org.junit.runner.RunWith;

import static androidx.test.espresso.Espresso.onView;
import static androidx.test.espresso.action.ViewActions.click;
import static androidx.test.espresso.assertion.ViewAssertions.matches;
import static androidx.test.espresso.matcher.ViewMatchers.isDisplayed;
import static androidx.test.espresso.matcher.ViewMatchers.withClassName;
import static androidx.test.espresso.matcher.ViewMatchers.withContentDescription;
import static androidx.test.espresso.matcher.ViewMatchers.withId;
import static androidx.test.espresso.matcher.ViewMatchers.withParent;
import static androidx.test.espresso.matcher.ViewMatchers.withText;
import static org.hamcrest.Matchers.allOf;
import static org.hamcrest.Matchers.is;

@LargeTest
@RunWith(AndroidJUnit4.class)
public class ScorePlusMinusTest {

    @Rule
    public ActivityTestRule<MainActivity> mActivityTestRule = new ActivityTestRule<>(MainActivity.class);

    @Test
    public void scorePlusMinusTest() {
        ViewInteraction appCompatImageButton = onView(
                allOf(withId(R.id.increaseTeam1), withContentDescription("Plus Button"),
                        childAtPosition(
                                childAtPosition(
                                        withClassName(is("android.widget.LinearLayout")),
                                        0),
                                3),
                        isDisplayed()));
        appCompatImageButton.perform(click());

        ViewInteraction textView = onView(
                allOf(withId(R.id.score_1), withText("1"),
                        withParent(withParent(IsInstanceOf.<View>instanceOf(android.widget.LinearLayout.class))),
                        isDisplayed()));
        textView.check(matches(withText("1")));

        ViewInteraction appCompatImageButton2 = onView(
                allOf(withId(R.id.decreaseTeam1), withContentDescription("Minus Button"),
                        childAtPosition(
                                childAtPosition(
                                        withClassName(is("android.widget.LinearLayout")),
                                        0),
                                0),
                        isDisplayed()));
        appCompatImageButton2.perform(click());

        ViewInteraction textView2 = onView(
                allOf(withId(R.id.score_1), withText("0"),
                        withParent(withParent(IsInstanceOf.<View>instanceOf(android.widget.LinearLayout.class))),
                        isDisplayed()));
        textView2.check(matches(withText("0")));
    }

    private static Matcher<View> childAtPosition(
            final Matcher<View> parentMatcher, final int position) {

        return new TypeSafeMatcher<View>() {
            @Override
            public void describeTo(Description description) {
                description.appendText("Child at position " + position + " in parent ");
                parentMatcher.describeTo(description);
            }

            @Override
            public boolean matchesSafely(View view) {
                ViewParent parent = view.getParent();
                return parent instanceof ViewGroup && parentMatcher.matches(parent)
                        && view.equals(((ViewGroup) parent).getChildAt(position));
            }
        };
    }
}
```

- 위 코드에서 아래 부분을 따로 본다면 이 부분에 대해서는 View를 찾고 이 부분에 대해서 perform을 하고 check를 하는 역할을 함

```java
ViewInteraction appCompatImageButton = onView(
                allOf(withId(R.id.increaseTeam1), withContentDescription("Plus Button"),
                        childAtPosition(
                                childAtPosition(
                                        withClassName(is("android.widget.LinearLayout")),
                                        0),
                                3),
                        isDisplayed()));
        appCompatImageButton.perform(click());
```

- 그 다음, 이 부분에 한해서 모든 요소들과 적절하게 맞는지에 대해서 확인할 수 있음

```java
ViewInteraction textView = onView(
                allOf(withId(R.id.score_1), withText("1"),
                        withParent(withParent(IsInstanceOf.<View>instanceOf(android.widget.LinearLayout.class))),
                        isDisplayed()));
        textView.check(matches(withText("1")));
```

- 그 다음에 이에 맞게 Matcher를 커스텀하여 만듬, 이런식으로 단 한 번에 recording을 통해서 다양한 상호작용이 가능했음

```java
private static Matcher<View> childAtPosition(
            final Matcher<View> parentMatcher, final int position) {

        return new TypeSafeMatcher<View>() {
            @Override
            public void describeTo(Description description) {
                description.appendText("Child at position " + position + " in parent ");
                parentMatcher.describeTo(description);
            }

            @Override
            public boolean matchesSafely(View view) {
                ViewParent parent = view.getParent();
                return parent instanceof ViewGroup && parentMatcher.matches(parent)
                        && view.equals(((ViewGroup) parent).getChildAt(position));
            }
        };
    }
```

- 이 부분에 대해서 이제 앞으로 Record를 활용하여서 테스트 코드에 대해서 다 정리해두거나 수정을 하여서 활용을 할 수가 있음 리사이클러뷰 등등 내가 적용한 부분에 대해서