## RelativeLayout
- 상대적으로 자식뷰의 위치를 정해줌, 기준을 중심으로 배치시킴
- 부모가 기준이 되거나 특정뷰가 될 수도 있음
- alignParent 속성을 통해서 위치를 조정할 수 있음, 부모뷰 기준으로
```XML
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="#F44336"
        android:layout_centerInParent="true"/>

    <TextView
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="#3F51B5"
        android:layout_alignParentBottom="true"/>

    <TextView
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="#3F51B5"
        android:layout_alignParentRight="true"/>

    <TextView
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="#3F51B5"
        android:layout_alignParentLeft="true"/>
    
    <TextView
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:background="#9C27B0"
        android:layout_alignParentEnd="true"/>

    <TextView
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:background="#9C27B0"
        android:layout_centerInParent="true"/>

    <TextView
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:background="#9C27B0"
        android:layout_centerHorizontal="true"/>

    <TextView
        android:layout_width="30dp"
        android:layout_height="30dp"
        android:background="#9C27B0"
        android:layout_centerVertical="true"/>

</RelativeLayout>
```

- 뷰끼리 상대적인 기준으로 옮기기 위해서는 다른 속성이 있음, 이를 위해 뷰를 구분하기 위해서 이름을 부여해줘야 함
```XML
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/view1"
        android:layout_centerInParent="true"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:background="#f23204"/>

    <TextView
        android:id="@+id/view2"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_toRightOf="@+id/view1"
        android:background="#CDDC39"/>

    <TextView
        android:id="@+id/view3"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_above="@id/view1"
        android:background="#CDDC39"/>

    <TextView
        android:id="@+id/view4"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_below="@id/view1"
        android:background="#CDDC39"/>

    <TextView
        android:id="@+id/view5"
        android:layout_width="50dp"
        android:layout_height="50dp"
        android:layout_toLeftOf="@id/view1"
        android:background="#CDDC39"/>

</RelativeLayout>
```