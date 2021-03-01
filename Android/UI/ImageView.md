## ImageView
- 이미지를 보여주는 뷰 컴포넌트
- src를 이용해서 Image를 보여줌, 경로를 표시할 땐 '@'를 사용함
- 이미지를 설정시 크기를 지정해주면 핸드폰의 해상도와 무관하게 고정되서 나오게 됨, 그래서 이 부분을 해상도별로 이미지를 쓰기도 함 
- 이를 해결하기 위해서 Android Drawable Importer를 활용함 
- Drawable Importer가 자동으로 해상도별로 이미지를 자동으로 생성해줌 
- 이미지 해상도를 미리 만들어서 파일을 미리 세팅을 해준다면 알아서 해상도에 맞춰서 설정해줌 
- scaleType을 활용하여서 고정 dp값을 가지고도 여백없이 만들 수 있긴함, 주로 centerCrop을 쓰면 이미지 뒤틀림없이 여백을 없앨 수 있음
```XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ImageView
        android:layout_width="300dp"
        android:layout_height="300dp"
        android:src="@drawable/ic_launcher_foreground"/>
    
    <ImageView
        android:layout_width="200dp"
        android:layout_height="200dp"
        android:background="#2196F3"
        android:scaleType="centerCrop"
        android:src="@drawable/dog"/>

</LinearLayout>
```