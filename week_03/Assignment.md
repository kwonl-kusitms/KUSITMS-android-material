# 3주차 과제
이번 주에는 안드로이드의 backend의 기본에 대해서 배웠죠? event와 listener, Toast 등의 message, 그리고 대망의 ListView에 대해서 배워봤습니다.

이번에 과제에서는 이런 것들을 이용해서, 저번주에 했던 instagram frontend를 더 programmatical하게 짜보죠!

## Instagram clone with backend
저번 과제를 하신 분들은 아시겠지만, 저희는 각각의 게시글 item을 Relative layout으로 만들고 이것들을 Linear layout에 배치했습니다. 이번에는 Relative layout을 이용해서 item의 layout을 만들고, ListView에 내용을 채워서 배치하도록 합시다! 사용하는 `res`는 저번시간과 같습니다.

[res file](../week_02/insta_res.zip)

위 파일을 다운로드하여 사용하세요! 이번에는 다음과 같이 item의 layout을 설정합시다. 저는 파일이름을 `feed_item.xml`이라 했습니다.

```xml
<!-- feed_item.xml -->

<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginTop="15dp" >

    <ImageView
        android:id="@+id/imageView"
        android:layout_width="400dp"
        android:layout_height="400dp"
        android:layout_centerHorizontal="true" />

    <TextView
        android:id="@+id/likeTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_below="@id/imageView"
        android:layout_alignStart="@id/imageView"
        android:layout_marginTop="15dp"
        android:textSize="20sp" />

    <CheckBox
        android:id="@+id/likeButton"
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:layout_below="@id/likeTextView"
        android:layout_alignStart="@id/imageView"
        android:layout_marginTop="10dp"
        android:background="@drawable/insta_like"
        android:button="@android:color/transparent" />

    <Button
        android:id="@+id/commentButton"
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:layout_below="@id/likeTextView"
        android:layout_marginStart="15dp"
        android:layout_marginTop="10dp"
        android:layout_toEndOf="@id/likeButton"
        android:background="@drawable/insta_comment" />

    <Button
        android:id="@+id/msgButton"
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:layout_below="@id/likeTextView"
        android:layout_marginStart="15dp"
        android:layout_marginTop="10dp"
        android:layout_toEndOf="@id/commentButton"
        android:background="@drawable/insta_msg" />

    <Button
        android:layout_width="40dp"
        android:layout_height="40dp"
        android:layout_below="@id/imageView"
        android:layout_alignEnd="@id/imageView"
        android:layout_marginTop="15dp"
        android:background="@drawable/insta_bookmark" />

    <TextView
        android:id="@+id/contentView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_below="@+id/likeButton"
        android:layout_alignEnd="@+id/imageView"
        android:layout_alignStart="@id/imageView"
        android:layout_marginTop="15dp"
        android:layout_marginBottom="20dp"
        android:textSize="20sp" />

</RelativeLayout>
```

이제 이 layout을 이용해서 인스타그램을 만들어보죠!

## Demo
![demo](images/app_sample.gif)

## Guide
1. Application 이름은 **Insta ListView**로, directory의 이름은 **02_assignment** 라고 지정해주세요.
2. 처음에 Button을 눌러야 feed가 로딩됩니다.
3. ListArray를 만들기 위한 `FeedItemData` class를 만들 때, `int imageId`, `int like`, `String content`를 member variable로 해놓으세요! 그리고나서 item을 더해줄 때 `items.add(new FeedItemData(R.drawable.sample1, 3, "첫 번째 피드!"));` 이런식으로 더해주면 됩니다. 왜냐하면 R.drawable.sample이라는 것도 결국은 정수형이거든요!!
4. 좋아요 버튼을 누를 때, Toast 대화창을 띄워주세요!
5. 좋아요 버튼이 눌리는 Listener는 어디서 달면 좋을까요? 아무래도 Data를 setting해줄 때 같이 해주면 좋겠죠? 즉, `Adapter` class의 `getView()`에서 해주도록 합시다! 이 때, `CheckBox.OnCheckedChangeListener`에 대한 설명은 저번 과제를 참고합시다.
6. like는 int인데 어떻게 String으로 변환할까요? 여러가지 방법이 있습니다. String.format을 사용할 수 있고, `Integer.toString(int)`를 통해서도 변환할 수 있습니다. 무엇을 사용하든 여러분의 자유!
7. 당연히 like에 대해서는 getter와 setter를 구현해야겠죠?
8. TextView에서는 `setText()`를 통해 내용을 바꿔줄 수 있었습니다. 그렇다면 ImageView에서는 어떻게 이미지를 바꿔줘야 할까요? 정답은 `setImageResource()`를 이용하는 것입니다. 구글링을 하면 쉽게 찾을 수 있죠 ㅎㅎ

## 마치며
이번 주 과제도 화이팅! Feel free to ask! 언제나 갠톡주세요! (부담스러운지 아무도 갠톡을 안함 ㅋ)