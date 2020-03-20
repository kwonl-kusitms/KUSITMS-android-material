# 2주차 과제
이번주에는 안드로이드에서 frontend가 무엇을 하는지 배우고, View, Layout, Widget, Drawable에 대해서 배워봤습니다. 이번주 과제에서는 간단한 앱의 frontend를 구현해보도록 합시다. 그리고, 예제로 보여드렸던 onClickListener를 이용해봅시다.

## Instagram Frontend
### 목표
인스타그램의 frontend를 구현해봅시다! 다음 gif와 같은 앱을 만들어봐요.

<img src="images/app_record.gif" style="width=500px;" />

### 구현해야 할 것
1. ScrollView를 이용하여 스크롤이 가능하도록 하세요
   1. ScrollView는 내부에 단 하나의 View를 포함합니다. 기본적으로는 LinearLayout이 들어가게 되니, 이것을 이용하세요.
2. ImageView를 이용해서 image를 표현하세요. ImageView의 소스는 android:background를 이용하세요!
3. LinearLayout에서, 하나의 카드는 Relative Layout으로 구현하는 것을 추천드립니다. 다른 Layout을 사용해도 상관 없습니다.
4. 좋아요가 눌리는 것은 state drawable을 사용하세요. 대신에 눌린상태로 유지되어야 하니, Button이 아니라 CheckBox를 사용해보세요! CheckBox에서 체크하는 박스를 없애는 방법은 다음 [링크](https://stackoverflow.com/a/20778832)를 참조하시고, Drawable에서는 state_pressed대신 state_checked를 사용해야겠죠?
5. 좋아요 100개, 좋아요를 누르면 101개로 바뀌는 것은 첫번째 카드에 대해서만 구현하시면 됩니다.
6. 좋아요 text가 바뀌는것에 대해서..어려우시면 다음의 code를 참고하세요! 자신의 view 이름에 맞도록 바꿔주시면 됩니다.

    ```java
    /* MainActivity.java 중 일부 */

    public class MainActivity extends AppCompatActivity {

        @Override
        protected void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setContentView(R.layout.activity_main);

            CheckBox likeButton1 = findViewById(R.id.likeButton1);
            likeButton1.setOnCheckedChangeListener(new CheckBox.OnCheckedChangeListener() {
                @Override
                public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
                    TextView likeTextView1 = findViewById(R.id.likeTextView1);
                    if (isChecked)
                        likeTextView1.setText("좋아요 101개");
                    else
                        likeTextView1.setText("좋아요 100개");
                }
            });
        }
    }
    ```

### Resources
[이 파일을 다운로드 하여 사용하세요!](insta_res.zip)