<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>CodeInsight</title>
<style>
body {
  background-color: #f5f7fa;
  font-family: "Segoe UI", sans-serif;
  margin: 0;
  padding: 0;
}
header {
  background: #0078d7;
  color: white;
  padding: 10px 20px;
  font-size: 20px;
}
main {
  display: flex;
  height: 90vh;
}
#editor, #review {
  flex: 1;
  padding: 20px;
}
#editor {
  background: #fff;
  border-right: 2px solid #ddd;
}
#review {
  background: #f9fafb;
}
textarea {
  width: 100%;
  height: 70%;
  font-family: monospace;
  font-size: 15px;
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 10px;
}
button {
  margin-top: 10px;
  padding: 8px 12px;
  background: #0078d7;
  color: white;
  border: none;
  border-radius: 4px;
}
button:hover { background: #005fa3; }
</style>
</head>
<body>
<header>🧠 CodeInsight - AI Code Reviewer</header>
<main>
  <section id="editor">
    <h3>Code Generator</h3>
    <select id="lang">
      <option value="c">C</option>
      <option value="cpp">C++</option>
    </select><br><br>
    <textarea id="code"></textarea><br>
    <button onclick="generate()">Generate</button>
    <button onclick="copyCode()">Copy</button>
  </section>

  <section id="review">
    <h3>AI Review</h3>
    <div id="result" style="background:white;border-radius:8px;padding:10px;height:70%;overflow:auto;border:1px solid #ccc;">
      Waiting for review...
    </div><br>
    <button onclick="review()">Review Code</button>
  </section>
</main>

<script>
const codeSamples = {
  c: `#include <stdio.h>
int main(){
  int a,b;
  printf("Enter two numbers: ");
  scanf("%d%d",&a,&b);
  printf("Sum = %d\\n", a+b);
  return 0;
}`,
  cpp: `#include <iostream>
using namespace std;
int main(){
  int a,b;
  cout << "Enter two numbers: ";
  cin >> a >> b;
  cout << "Product = " << a*b << endl;
  return 0;
}`
};

function generate(){
  const lang = document.getElementById("lang").value;
  document.getElementById("code").value = codeSamples[lang];
  document.getElementById("result").innerText = "✅ Code generated successfully.";
}

function review(){
  const code = document.getElementById("code").value;
  let warn = [];
  if(code.includes("gets")) warn.push("⚠️ Dangerous function 'gets'.");
  if(!code.includes("return")) warn.push("ℹ️ Add 'return 0;'");
  if(warn.length===0) warn.push("✅ No major issues found!");
  document.getElementById("result").innerText = warn.join("\\n");
}

function copyCode(){
  const area = document.getElementById("code");
  area.select(); document.execCommand("copy");
  document.getElementById("result").innerText = "📋 Code copied!";
}
</script>
</body>
</html>
