# 6주차 과제
6주차에 네트워킹까지 마치고, 우리는 안드로이드에 대해서 어느정도는 마스터 했습니다.

진도가 많이 빨랐지만, 그래도 복습을 열심히 하시면 충분히 따라올 수 있었을 거라 생각합니다! 안드로이드 최종 과제는 (반쯤) 완벽한 인스타그램 구현입니다.

## Instagram with bottom navigation view
**Bottom navigation view의 경우, 본인이 Fragment가 너무 어려워서 구현이 불가능할 것 같다면 건너 뛰어도 됩니다!**

저번 시간에 bottom navigation view에 대해서 배웠죠? 우리가 과제로 만들었던 instgram listView 을 bottom navigation view에 적용시켜봅시다. `Home`, `Search`, `Like`의 총 세 개의 버튼을 구현하되, `Search`와 `Like`는 fragment의 가운데에 TextView만 띄워놔도 충분합니다.

## Instgram with Networking!
위와 같이 bottom navigation view를 구현하셨다면, 이제 network를 이용해 피드를 채워보도록 합시다.

> [https://raw.githubusercontent.com/kwonl-kusitms/api-for-assignment/master/feed.json](https://raw.githubusercontent.com/kwonl-kusitms/api-for-assignment/master/feed.json)

위 링크를 통해서 피드의 정보를 받아오도록 합시다. Response는 다음과 같습니다.

```json
[
    {
        "content": "첫 번째 피드",
        "like": 3,
        "image": "https://raw.githubusercontent.com/kwonl-kusitms/api-for-assignment/master/food1.jpeg"
    },
    {
        "content": "두 번째 피드",
        "like": 4,
        "image": "https://raw.githubusercontent.com/kwonl-kusitms/api-for-assignment/master/food2.jpeg"
    },
    {
        "content": "첫 번째 피드",
        "like": 5,
        "image": "https://raw.githubusercontent.com/kwonl-kusitms/api-for-assignment/master/food3.jpeg"
    }
]
```

이 response를 받았다면, content와 like는 그대로 채워도 되지만, image의 경우 return된 url을 바탕으로 한번 더 request를 보내야 합니다. Volley의 `ImageRequest`의 경우 다음 코드를 참고하세요!

```java
ImageRequest imageRequest = new ImageRequest(
        object.getString("image"),
        new Response.Listener<Bitmap>() {
            @Override
            public void onResponse(Bitmap response) {
                try {
                    items.add(new FeedItemData(
                            response,
                            object.getInt("like"),
                            object.getString("content")
                    ));
                    feedItemAdapter.notifyDataSetChanged();
                } catch (JSONException e) {
                    Log.d(TAG, "onResponse: " + e.getMessage());
                }
            }
        }, 0, 0, null, Bitmap.Config.RGB_565,
        new Response.ErrorListener() {
            @Override
            public void onErrorResponse(VolleyError error) {
                Log.d(TAG, "onErrorResponse: " + error.getMessage());
            }
        }
);
```

위 코드와 같이 `ImageRequest`를 이용할 수 있고, 잘 보시면 아시겠지만 `FeedItemData` class가 저번 시간과는 조금 달라야 할 것입니다.

원래의 `FeedItemData`에서, `imageId`라는 member variable을 통해 image를 전달했다면, 이번에는 `Bitmap image`라는 member variable로 대처하여야 합니다. 다음과 같이요!

```java
public class FeedItemData {
    private Bitmap image;
    private int like;
    private String content;

    public FeedItemData(Bitmap image, int like, String content) {
        this.image = image;
        this.like = like;
        this.content = content;
    }

    public Bitmap getImage() {
        return image;
    }

    public void setImage(Bitmap image) {
        this.image = image;
    }

    public int getLike() {
        return like;
    }

    public void setLike(int like) {
        this.like = like;
    }

    public String getContent() {
        return content;
    }
}
```

이후에, 다음과 같이 `ImageView`에 이미지를 설정할 수 있습니다.

```java
ImageView imageView = view.findViewById(R.id.imageView);
imageView.setImageBitmap(feedItem.getImage());
```

## 결과물
사진을 바꾸봤습니다 ㅎㅎ. 제가 찍은 사진들입니다!

![결과 gif](images/app_sample.gif)

인터넷에서 받아오는 것이기 때문에, 화면 로딩에 많은 시간이 소요될 수 있습니다! 이상하다 싶으면 log를 실행시켜가면서 코드가 의도한대로 돌아가는지 시험해보세요!

## 추신
이번 과제는 매우매우매우 어려울 수 있습니다. 좀더 쉽게 내보려고 했는데, 제 능력이 부족하여 더 쉽게 내기가 힘드네요..

따라서 방학 때 그동안 했던 것을 많이 복습하고, 구글링을 통해 찾아보면서 과제를 하기를 바랍니다. 저한테 갠톡하거나 물어보는 것도 망설이지 말고 해주세요!

그럼에도 불구하고 시간이 없거나 너무 어려우신 분들은, 이번 과제는 건너뛰어도 될 것 같습니다. 대신에 제가 만들어놓은 코드를 드릴테니, **반드시 읽어보시고 이해** 해보시는 것을 추천드립니다.

> [https://github.com/kwonl-kusitms/KUSITMS_21th-android_study/tree/master/03_assignment](https://github.com/kwonl-kusitms/KUSITMS_21th-android_study/tree/master/03_assignment)

직접 clone해서 실행해봐도 좋습니다. 다음과 같은 command를 통해서 제 프로젝트를 여러분의 local에 다운받을 수 있습니다.

```bash
cd {원하는 directory로 들어가세요!}
git clone https://github.com/kwonl-kusitms/KUSITMS_21th-android_study
```

위와 같이 clone한 뒤, 안드로이드 프로젝트를 열 때 03_assignment를 찾아 열어주시면 됩니다. 이후에 자유롭게 둘러보며 코드를 이해해보세요!

방학 끝나고 봐요 다들~