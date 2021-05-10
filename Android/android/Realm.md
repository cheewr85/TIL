## Realm
- 좀 더 복잡한 데이터베이스를 사용하기 위해서 Realm 라이브러리를 사용할 것임
- 매우 큰 라이브러리임
- 실습
```kotlin
package techtown.org.fastcampus

import io.realm.RealmObject

// realm을 사용하기 위해서 데이터베이스 테이블을 만들어야함, 아래와 같은 테이블
// 이름 학번 학교 성별 -> 필드명
// 홍길동 1 서울 남
// 김진짜 2 전북 여

// 필드명을 적어줄 것임, 필드들의 각각의 타입이 있음
open class School : RealmObject() { // 해당 클래스를 open을 통해서 열어줘야함
    var name : String? = null
    var location : String? = null
}
```

```kotlin
package techtown.org.fastcampus

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.util.Log
import io.realm.Realm
import io.realm.RealmConfiguration
import kotlinx.android.synthetic.main.activity_relam.*

class RelamActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_relam)

        // Realm을 초기화함
        Realm.init(this@RelamActivity)
        // 이런 방식으로 초기화하게끔 해주는 configuration 사용
        // .으로 계속 이어나가는 것을 메소드 체이닝이라고 함, 빌더 패턴에 많이 들어감
        val config : RealmConfiguration = RealmConfiguration.Builder() // configuration을 사용하고 builder를 가져옴
                // 기존 데이터베이스 맨 위의 필드값의 변경이 생기면 데이터를 지워버린다는 의미
            .deleteRealmIfMigrationNeeded() // 가져온 builder에서 Migration이 필요한 경우 realm 지우게끔 설정, Migration은 데이터 베이스를 동기화 시키는 것임, 무엇인가 추가할 때 합치기 위해서
            .build()
        Realm.setDefaultConfiguration(config)
        val realm = Realm.getDefaultInstance() // realm을 불러옴

        button_save.setOnClickListener{
            realm.executeTransaction{ // transaction을 실행함, Transaction은 DB 용어, 여러가지 조합할 수 있음,각각의 데이터를 뽑아서 하나의 테이블에서 합칠 수 있음
                // Transaction을 통해서 중간에 데이터가 변경될 수 있는 상황을 미연의 방지 작업단위를 아예 묶어버림, 기존에 배운 것 기준으로 begin ~ commit을 아예 묶어버리는 것임
                // A테이블에서 데이터를 가져온다 -> 10
                // B테이블에서 데이터를 가져온다
                // C테이블에서 데이터를 가져온다
                // 조합을 한다
                // D테이블에 저장을 한다
                with(it.createObject(School::class.java)) { // this는 스쿨 class임, with으로 묶어버림
                    // 아래와 같이 object를 만들어 데이터를 생성하여 넣어줌
                    this.name = "어떤 대학교"
                    this.location = "서울"
                }

            }
        }

        button_load.setOnClickListener{
            realm.executeTransaction { // realm 통해서 접근시 항상 execute 사용
                // 데이터를 찾아올 때는 해당 테이블에 가서, 그곳에서 데이터를 꺼내와야함
                val data = it.where(School::class.java).findFirst() // school 테이블에 가서 테이블의 첫 번째 줄을 가져옴
                Log.d("data","data : " + data)
            }
        }

        button_delete.setOnClickListener{
            realm.executeTransaction{
                // 지우는것도 마찬가지로 해당 테이블에 가서 찾은 다음에 그 데이터를 지워야함
                it.where(School::class.java).findAll().deleteAllFromRealm() // 모두 다 찾아서 모두 다 삭제 해버림
//                it.where(School::class.java).findFirst()?.deleteFromRealm() // 첫번째 것만 찾아서 삭제함
            }
        }
    }

}
```