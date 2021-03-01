## FrameLayout
- FrameLayout도 부모 레이아웃의 역할을 할 수 있음
- 특징 중 하나가 자식으로 가지고 있는 것들을 겹치게 할 수 있음
- FrameLayout에 있는 자식뷰들이 겹쳐서 볼 수 있음 
- 먼저 적은 뷰가 맨 아래에 있음, 하나둘 적어나가면서 쌓여나감
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <LinearLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="30dp"
            android:text="hello"
            android:background="#3F51B5"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="30dp"
            android:text="hello"
            android:background="#673AB7"/>

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:textSize="30dp"
            android:text="hello"
            android:background="#FFEB3B"/>

    </LinearLayout>

    <FrameLayout
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="100dp">

        <TextView
            android:layout_width="300dp"
            android:layout_height="300dp"
            android:textSize="30dp"
            android:text="hello"
            android:background="#3F51B5"/>

        <TextView
            android:layout_width="200dp"
            android:layout_height="200dp"
            android:textSize="30dp"
            android:text="hello"
            android:background="#673AB7"/>

        <TextView
            android:layout_width="100dp"
            android:layout_height="100dp"
            android:textSize="30dp"
            android:text="hello"
            android:background="#FFEB3B"/>

    </FrameLayout>

</LinearLayout>
```

- RelativeLayout도 뷰를 겹칠 수 있음
```XML
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:background="#3F51B5"/>

    <TextView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="#9C27B0"/>

    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#009688"/>

</RelativeLayout>
```

- 뷰를 겹쳐서 만들고 싶을 때, RelativeLayout, FrameLayout을 활용하면 됨
- FrameLayout을 사용하는것이 더 좋긴함
- 만일 실제로 구동시 연산을 할 때 RelativeLayout이 더 많은 연산을 하므로 좀 더 느린 부분이 있음, 상대적인 위치를 잡기 때문에(단 눈에 보일 정도의 수준은 아님)