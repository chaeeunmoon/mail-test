<template>
  <div class="container">
    <div class="title">
      <h2 class="title_txt">문의하기 테스트 하기</h2>
    </div>
    <article class="form_group">
      <label for="name">이름</label>
      <input type="text" name="name" id="name" placeholder="이름">
    </article>
    <article class="form_group">
      <label for="name">내용</label>
      <textarea name="desc" id="desc" rows="5" placeholder="문의 상세 내용"></textarea>
    </article>
    <article>
      <button @click="submitForm()">전송하기</button>
    </article>
  </div>
</template>

<script>
export default {
  name: 'Form',
  props: {
    //msg: String
  },
  methods: {
    // 슬랙 메시지 보내기
    submitForm(){
      console.log('click');
        var BaseUrl = "https://hooks.slack.com/services/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";
        var name = document.getElementById("name").value;
        var phone = document.getElementById("desc").value;

        var xhr = new XMLHttpRequest();
        xhr.open("POST", BaseUrl, true);

        //Send the proper header information along with the request
        xhr.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

        xhr.onreadystatechange = function() { // Call a function when the state changes.
            if (this.readyState === XMLHttpRequest.DONE && this.status === 200) {
                // Request finished. Do processing here.
            }
        }
        var payload = {
            "text": "슬렉 메시지 보내기",
            "blocks": [
                {
                    "type": "section",
                    "text": {
                    "type": "mrkdwn",
                    "text": "🛎 *입점 문의* "
                    }
                },
                {
                    "type": "section",
                    "block_id": "section123",
                    "fields": [
                        {
                            "type": "mrkdwn",
                            "text": "> *Q1. 이름*\n"+ name +"\n\n*Q2. 상세내용*\n"+ phone +"\n\n"
                        }
                    ]
                }
            ]
        };
        xhr.send( JSON.stringify(payload));   
    }

      
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@font-face {
    font-family: 'IM_Hyemin-Bold';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2106@1.1/IM_Hyemin-Bold.woff2') format('woff');
    font-weight: normal;
    font-style: normal;
}

.container {
  max-width: 100%;
  width: 500px;
  margin: 0 auto;
}

.title > .title_txt {
  font-family: 'IM_Hyemin-Bold';
  text-align: center;
  font-size: 30px;
}

.form_group { margin-bottom: 10px; }

.form_group label {
  font-family: 'IM_Hyemin-Bold';
  display: block;
  font-size: 18px;
  text-align: left;
  margin-bottom: 0.5em;
}

.form_group input,
.form_group textarea {
  font-family: 'IM_Hyemin-Bold';
  font-size: 17px;
  width: 100%;
  border: 1px solid #c8c8c8;
  border-radius: 8px;
  padding: 0.6em;
}

button {  
  outline: none;
  font-family: 'IM_Hyemin-Bold';
  font-size: 20px;
  background-color: #34BE82;
  color: #fff;
  width: 300px;
  text-align: center;
  border: none;
  border-radius: 8px;
  padding: 0.6em;
  margin-top: 0.5em;
}
</style>
