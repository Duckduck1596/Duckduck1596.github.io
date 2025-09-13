#RSS_Summary_Service만들기

오늘은 데일리세큐 RSS를 요약해 MP3파일로 저장하는 자동화 파일을 만들어 보았다  몇몇 헷갈리는 부분이 있었다.

우선 처음 파서 배울 때 리스크 만들어서 append해 파일로 만들었는데 파싱할 때는 append 보단 getattr을 이용해 혹시 내용이 없을 경우 없다고 표기할 수 있다는 것을 알았따 또한 반목문에서 append를 작동했더니 따로 만든 리스트에 중첩되어 저장된다는 것을 느끼고 반복문 안에 변수를 선언해 getattr로 내용을 불러와야한다는 것을 알았다.




```
import feedparser
from gtts import gTTS

url = "https://www.dailysecu.com/rss/allArticle.xml"
feed = feedparser.parse(url)

texts = []


for entry in feed.entries[:3]:
   title = getattr(entry, "title", "제목 없음")
   summary = getattr(entry, "summary", "제목없음")

   texts.append(f"제목: {title}\n내용: {summary}\n")


merge_texts = "\n".join(texts)

#파일내용 확인
print(merge_texts)

tts = gTTS(merge_texts, lang="ko")
tts.save("dailysecu_news.mp3")

print("파일 변환 완료. dailysecu_news.mp3 파일이 생성되었습니다.")
```
