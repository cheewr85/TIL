## Drawable
- Drawable 파일을 직접 만들 수 있음
- xmlns:android="http://schemas.android.com/apk/res/android" 을 통해서 'android:'로 시작하는 옵션을 쓸 수 있음 
- Drawable 파일을 만들어 그라데이션 효과를 직접 만들 수 있음, 그라데이션 같은 경우는 직접 그려서 사용하는 것이 좋음 
```XML
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <gradient
        android:angle="180"
        android:centerColor="#9C27B0"
        android:endColor="#2196F3"
        android:startColor="#00BCD4"/>

</shape>
```

- stroke를 통해서 선을 그어줄 수 있음, 테두리를 그릴 수 있음
```XML
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <stroke
        android:width="20dp"
        android:color="#2196F3"/>
    
</shape>
```

- solid를 통해 면을 그릴 수 있음, 가운데와 테두리를 따로 따로 그릴 수 있음 
```XML
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="oval">

    <solid
        android:color="#2196F3"/>
    <stroke
        android:width="30dp"
        android:color="#ffffff"/>

</shape>
```

- radius는 모서리를 둥글게 만들 수 있음, corner 기능을 활용하여서 사용가능
```XML
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle">

    <solid
        android:color="#03A9F4"/>

    <corners
        android:bottomLeftRadius="30dp"
        android:bottomRightRadius="20dp"
        android:topLeftRadius="50dp"
        android:topRightRadius="100dp"/>

</shape>
```