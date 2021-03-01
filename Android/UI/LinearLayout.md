## LinearLayout
- Design탭 내의 Layouts, 부모 컴포넌트가 될 수 있는 부분임
- 주로 화면을 구성하는 역할(배치), 화면에 직접적으로 나오는 역할은 하지 않음 
- 자식 컴포넌트로 사용되는 것들은 실질적으로 화면에 나옴, 직접적으로 위치를 바꾸기도 힘듬
- LinearLayout에 의해서 위치가 정해짐 orientation(속성) -> 자식 컴포넌트의 배치(위치)를 바꿀 수 있음(수직, 수평)
- LinearLayout을 부모 뷰로 가지고 있기 때문에 TextView가 layout_gravity라는 속성을 가질 수 있음, 해당 뷰의 배치를 정하는 속성을 지님
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:text="안녕하세요"
        android:layout_gravity="bottom"
        android:textColor="@color/design_default_color_primary"
        android:textSize="20dp"
        android:layout_height="wrap_content"/>



</LinearLayout>
```

- 만일 부모 레이아웃에 gravity 속성을 두면 그 자식뷰가 모두 gravity의 영향을 받아서 배치가 됨(일괄적으로)
- 하지만 아래의 TextView처럼 layout_gravity를 left로 하면 left로 감
- 즉 여기서 만일 속성이 중복 적용될 경우 더 작은 범주가 적용이 됨, 즉 TextView의 범위가 더 작으므로 왼쪽으로 혼자 빠지는 것임
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="right"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
				android:layout_gravity="left"
        android:text="안녕하세요"
        android:textColor="@color/design_default_color_primary"
        android:textSize="20dp"
        android:layout_height="wrap_content"/>

		<TextView
		        android:layout_width="wrap_content"
		        android:text="안녕하세요"
		        android:textColor="@color/design_default_color_primary"
		        android:textSize="20dp"
		        android:layout_height="wrap_content"/>




</LinearLayout>
```

- 안드로이드에서 색깔을 정할때는 RGB 칼라코드로 16진수로 사용함
- 아래의 예시에서 width은 폭을, height는 길이를 의미함
- 숫자 입력도 가능하지만 match_parent 즉, 최상위뷰의 가로폭만큼 사용하는 것(레이아웃은 핸드폰의 가로폭을 모두 사용하겠다는것)
- wrap_content는 글씨를 감쌀 수 있을만큼의 폭으로 할 것임을 의미함
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <ImageView
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="#2196F3"/>

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="안녕하세요"
        android:textSize="60dp"
        android:background="#E91E63"/>



</LinearLayout>
```

### 실습
- layout_gravity는 부모 클래스 기준으로 어디로 갈 지 정하는 것이고 
- gravity는 TextView가 가지고 있는 컨텐츠를 어디로 보낼지 정하는 것임 
- 두가지 속성을 모두 적용하고 싶다면 '|'를 쓰면 됨
- layout_weight을 활용하여 핸드폰마다 보여지는 다른 크기에 대해서 비율을 설정해서 보일 수 있도록 설정함, 주로 이 상태에서 width를 0dp로 둠
- weightSum 속성은 전체비율을 말함, 전체를 해당 값만큼 나눠서 함
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:textSize="20dp"
        android:text="가운데"/>

    <TextView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:gravity="right|center"
        android:text="Gravity"/>

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="100"
            android:textSize="20dp"
            android:background="#3F51B5"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="100"
            android:textSize="20dp"
            android:background="#CDDC39"/>
        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="100"
            android:textSize="20dp"
            android:background="#E91E63"/>

    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <TextView
            android:layout_weight="1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:text="100"
            android:textSize="20dp"
            android:background="#3F51B5"/>
        <TextView
            android:layout_weight="1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:text="200"
            android:textSize="20dp"
            android:background="#CDDC39"/>
        <TextView
            android:layout_weight="1"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:text="300"
            android:textSize="20dp"
            android:background="#E91E63"/>


    </LinearLayout>

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="300dp"
        android:weightSum="5"
        android:orientation="vertical">
        <TextView
            android:layout_weight="1"
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:text="100"
            android:textSize="20dp"
            android:background="#3F51B5"/>
        <TextView
            android:layout_weight="1"
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:text="200"
            android:textSize="20dp"
            android:background="#CDDC39"/>
        <TextView
            android:layout_weight="1"
            android:layout_width="wrap_content"
            android:layout_height="0dp"
            android:text="300"
            android:textSize="20dp"
            android:background="#E91E63"/>
    </LinearLayout>

</LinearLayout>
```