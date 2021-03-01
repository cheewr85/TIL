## Scrollview
- 스크롤을 내릴 수 있는 컴포넌트
- 스크롤뷰는 오직 하나의 자식뷰만을 가질 수 있음, 그러므로 여기서 자식뷰를 다른 뷰 컨테이너를 활용해서 쓰면 됨 
- 스크롤바를 없앨 수도 있음, 해당 속성 활용(android:scrollbars="none")
- 스크롤뷰를 만들 때 fillViewport를 활용하여서 예기치 못한 에러를 방지하면 좋음(android:fillViewport="true")
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ScrollView
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:scrollbars="none"
        android:fillViewport="true">

        <LinearLayout
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:orientation="vertical">

            <TextView
                android:layout_width="300dp"
                android:layout_height="300dp"
                android:background="#3F51B5"/>

            <TextView
                android:layout_width="200dp"
                android:layout_height="200dp"
                android:background="#673AB7"/>

            <TextView
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:background="#03A9F4"/>

            <TextView
                android:layout_width="300dp"
                android:layout_height="300dp"
                android:background="#3F51B5"/>

            <TextView
                android:layout_width="200dp"
                android:layout_height="200dp"
                android:background="#673AB7"/>

            <TextView
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:background="#03A9F4"/>

            <TextView
                android:layout_width="300dp"
                android:layout_height="300dp"
                android:background="#3F51B5"/>

            <TextView
                android:layout_width="200dp"
                android:layout_height="200dp"
                android:background="#673AB7"/>

            <TextView
                android:layout_width="100dp"
                android:layout_height="100dp"
                android:background="#03A9F4"/>

        </LinearLayout>
    </ScrollView>

</LinearLayout>
```