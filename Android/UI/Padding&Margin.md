## Padding & Margin
- Margin을 주게 되면 부모뷰로부터 Margin을 준만큼 떨어지게 됨 
- Padding은 자식 뷰 기준으로 자식뷰가 가지고 있는 컨텐츠를 어떻게 떨어뜨리느냐의 관점, 내용물을 안으로 움직이는 것, 컨텐츠의 여백을 정함
- layout_margin의 경우 Top, Left, Right, Bottom을 200dp 준 것과 동일한 효과임
- layout_padding의 경우도 마찬가지
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <TextView
        android:layout_marginTop="20dp"
        android:layout_marginLeft="50dp"
        android:layout_marginRight="100dp"
        android:layout_marginBottom="200dp"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#00BCD4"
        android:text="안녕하세요"/>


    <TextView
        android:paddingLeft="10dp"
        android:paddingTop="30dp"
        android:padding="20dp"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:background="#F44336"
        android:text="안녕하세요"/>
    
    <TextView
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:layout_margin="100dp"
        android:background="#FFC107"/>

</LinearLayout> 
```