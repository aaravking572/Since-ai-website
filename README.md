<!DOCTYPE html>
<html>
<head>
  <title>AskAnything AI</title>
  <style>
    body { font-family: Arial; padding: 40px; background: #f5f5f5; }
    #question { width: 80%; padding: 10px; }
    button { padding: 10px 20px; }
    #answer, #explanation { margin-top: 20px; background: #fff; padding: 15px; border-radius: 5px; }
  </style>
</head>
<body>
  <h1>Ask Anything</h1>
  <input type="text" id="question" placeholder="Ask your question...">
  <button onclick="askQuestion()">Ask</button>
  <div id="answer"></div>
  <div id="explanation"></div>

  <script>
    async function askQuestion() {
      const question = document.getElementById("question").value;
      const res = await fetch("/ask", {
        method: "POST",
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({ question })
      });
      const data = await res.json();
      document.getElementById("answer").innerHTML = "<b>Answer:</b><br>" + data.answer;
      document.getElementById("explanation").innerHTML = "<b>How it works:</b><br>" + data.explanation;
    }
  </script>
</body>
</html> 
from flask import Flask, request, jsonify
import openai

app = Flask(__name__)
openai.api_key = "your-api-key-here"

@app.route("/ask", methods=["POST"])
def ask():
    data = request.get_json()
    question = data["question"]

    # Ask for the answer
    answer_response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": question}]
    )

    # Ask for explanation of how it was solved
    explanation_response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": f"Explain how you answered this question: {question}"}]
    )

    return jsonify({
        "answer": answer_response.choices[0].message.content,
        "explanation": explanation_response.choices[0].message.content
    })

if __name__ == "__main__":
    app.run(debug=askverse-ai/
├── app.py               # Flask backend
├── templates/
│   └── index.html       # Frontend HTML
├── static/
│   └── style.css        # CSS file
└── requirements.txt     # <!DOCTYPE html>
<html>
<head>
  <title>AskVerse AI</title>
  <link rel="stylesheet" href="/static/style.css">
</head>
<body>
  <div class="container">
    <h1>AskVerse AI</h1>
    <input type="text" id="questionInput" placeholder="Ask anything...">
    <button onclick="askQuestion()">Ask</button>
    <div id="result">
      <h2>Answer</h2>
      <p id="answer"></p>
      <h3>How it was solved</h3>
      <p id="explanation"></p>
    </div>
  </div>

  <script>
    async function askQuestion() {
      const question = document.getElementById("questionInput").value;
      const res = await fetch("/ask", {
        method: "POST",
        headers: {"Content-Type": "application/json"},
        body: JSON.stringify({question})
      });
      const data = await res.json();
      document.getElementById("answer").innerText = data.answer;
      document.getElementById("explanation").innerText = data.explanation;
    }
  </script>
</body>
</html>
body {
  font-family: 'Arial', sans-serif;
  background: #101010;
  color: white;
  display: flex;
  justify-content: center;
  padding: 40px;
}
.container {
  width: 80%;
  max-width: 800px;
}
input {
  width: 100%;
  padding: 12px;
  font-size: 18px;
  margin-bottom: 10px;
}
button {
  padding: 12px 24px;
  background: #0080ff;
  color: white;
  border: none;
  cursor: pointer;
  font-size: 16px;
}
button:hover {
  background: #0055aa;
}
#result {
  margin-top: 20px;
  background: #202020;
  padding: 20px;
  border-radius: 8px;
}
