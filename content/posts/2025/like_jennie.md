---
date: '2025-03-21T15:48:27+13:00'
draft: false
title: 'Make It Yours! 🎵 Personalising the Lyrics to Like Jennie 🎤'
categories: ["k-pop", "blackpink", "jennie", "ruby", "album", "odd atelier", "github"]
---

## Interactive Personalisations to the Lyrics of Like Jennie! 🤗

Jennie is a member of the K-pop group [BLACKPINK](https://ygfamily.com/ko/artists/blackpink/profile) who recently released her solo album [Ruby](https://en.wikipedia.org/wiki/Ruby_(Jennie_album)) 🎧🎵

`Like Jennie` is a song in the new album Ruby!

![alt text](/assets/images/like_jennie_like_someone.PNG)

In this [YouTube video](https://youtu.be/Dz77zxY3NJE?t=1146), Jennie explains the meaning behind the song [Like Jennie](https://genius.com/Jennie-like-jennie-lyrics) - and how it can be personalised for anyone 😁!

This post is to help anyone personalise the song `Like Jennie`!

Enter text in the boxes below and click `SUBMIT` button! 

The text you enter will update the lyrics to the song `Like Jennie` and the updated lyrics will appear after you hit the `SUBMIT` button 😎!

All the fields are required 😉 you can listen to the song [here](https://www.youtube.com/watch?v=aS7al94FVbk) while filling out the fields below!

<style>
  input[type="text"] {
    color: black;
    background-color: white;
    border: 1px solid #ccc;
    border-radius: 4px;
    padding: 10px;
    width: 100%;
    max-width: 400px;
    margin-bottom: 10px;
  }

  @media (prefers-color-scheme: dark) {
    input[type="text"] {
      color: white;
      background-color: #333;
    }
  }
</style>

<form id="textForm" style="margin-bottom: 20px;">
  <label for="username" style="display: block; margin-bottom: 10px;">Enter your first name:</label>
  <input type="text" id="username" name="username" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">
  
  <label for="jobVerb" style="display: block; margin-bottom: 10px;">Enter a verb that best explains your job (e.g. code, consult, sing):</label>
  <input type="text" id="jobVerb" name="jobVerb" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">

  <label for="jobVerbing" style="display: block; margin-bottom: 10px;">Now take the above verb and make it describe the action in progress  (e.g. coding, consulting, singing):</label>
  <input type="text" id="jobVerbing" name="jobVerbing" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">

  <label for="job" style="display: block; margin-bottom: 10px;">Enter your job title:</label>
  <input type="text" id="job" name="job" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">

  <label for="mustDos" style="display: block; margin-bottom: 10px;">Enter two things you do as part of your job, try to make it rhyme! 🎧🎸 (e.g. functions clean, system lean):</label>
  <input type="text" id="mustDos" name="mustDos" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">
  
  <label for="goal" style="display: block; margin-bottom: 10px;">Enter your daily objective in two words (e.g. green build):</label>
  <input type="text" id="goal" name="goal" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">
  
  <label for="tool" style="display: block; margin-bottom: 10px;">Enter what you need for your daily objective (e.g. DevOps):</label>
  <input type="text" id="tool" name="tool" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">

  <label for="desire" style="display: block; margin-bottom: 10px;">Enter your desire in one word:</label>
  <input type="text" id="desire" name="desire" style="padding: 10px; width: 100%; max-width: 400px; margin-bottom: 10px; border: 1px solid #ccc; border-radius: 4px;">
  
  <button type="button" onclick="updateText()" style="padding: 10px 20px; background-color: #007bff; color: white; border: none; border-radius: 4px; cursor: pointer;">Submit</button>
</form>

<div id="outputText" style="font-weight: bold;"></div>

<div id="lyrics" style="display: none;">
  <p>[Verse 1]<br>
  Special edition and your AI couldn't copy<br>
  I'm leaving clues in the fittin' room and it's hot tea<br>
  No, I'm not thinking about no exes, know they miss me<br>
  I got the whole room spinning like it's tipsy<br>
  Don't bore us, take you to the chorus</p>

  <p>[Chorus]<br>
  Who wanna {{jobVerb}} with {{name}}?<br>
  Keep your {{mustDos}} like {{name}}<br>
  Who else got 'em {{jobVerbing}} like {{name}}?<br>
  Like, like, like ({{name}}, {{name}}, {{name}}, {{name}})<br>
  I think I really like ({{name}}, {{name}}, {{name}})<br>
  Haters, they don't really like ({{name}}, {{name}}, {{name}}, {{name}})<br>
  'Cause they could never ever be ({{name}}, {{name}}, {{name}})<br>
  But have you ever met {{name}}, {{name}}, {{name}}, {{name}}?<br>
  {{name}}, {{name}}, {{name}}<br>
  It's {{name}}, {{name}}, {{name}}, {{name}}, {{name}}</p>

  <p>[Post-Chorus]<br>
  But have you ever met?<br>
  But have you ever met?<br>
  But have you ever met?<br>

  <p>[Verse 2]<br>
  얼말 줘도 못해 서커스짓<br>
  {{jobVerbing}}한번에 만들어 {{goal}}<br>
  They can't deal with me 'cause I'm priceless<br>
  여러 {{job}}들 속에 내 DNA<br>
  Get, get outta my way<br>
  바비가 처키가 되기 전에<br>
  Name, shame, blame tryna burst my bubble<br>
  터트려봐 그럼 더 큰 {{desire}}에서<br>
  만나는 거야 {{name}}를 keep shading<br>
  {{goal}}엔 필요해 {{tool}}<br>
  I've slayed it, and I graved it<br>
  Yes, I'm guilty 잘난 게 죄니</p>

  <p>[Chorus]<br>
  Who wanna {{jobVerb}} with {{name}}?<br>
  Keep your {{mustDos}} like {{name}}<br>
  Who else got 'em {{jobVerbing}} like {{name}}?<br>
  Like, like, like<br>
  I think I really like {{name}}<br>
  Haters, they don't really like {{name}}<br>
  'Cause they could never ever be {{name}}<br>
  But have you ever met {{name}}, {{name}}, {{name}}, {{name}}?<br>
  {{name}}, {{name}}, {{name}}<br>
  It's {{name}}, {{name}}, {{name}}, {{name}}<br>
  {{name}}, {{name}}, {{name}}<br>
  Like {{name}}, {{name}}, {{name}}, {{name}}, {{name}}<br>
  {{jobVerb}} with {{name}}<br>
  Keep your {{mustDos}} done like {{name}}<br>
  Who else got 'em {{jobVerbing}}, like {{name}}</p>

  <p>[Post-Chorus]<br>
  But have you ever met {{name}}?<br>
  But have you ever met?<br>
  {{name}}, {{name}}, {{name}}<br>
  It's {{name}}, {{name}}, {{name}}, {{name}}</p>
</div>

<script>
  function updateText() {
    var username = document.getElementById('username').value;
    var jobVerb = document.getElementById('jobVerb').value;
    var jobVerbing = document.getElementById('jobVerbing').value;
    var mustDos = document.getElementById('mustDos').value;
    var desire = document.getElementById('desire').value;
    var job = document.getElementById('job').value;
    var goal = document.getElementById('goal').value;
    var tool = document.getElementById('tool').value;
    
    var lyrics = document.getElementById('lyrics').innerHTML;
    var updatedLyrics = lyrics
      .replace(/{{name}}/g, username)
      .replace(/{{jobVerb}}/g, jobVerb)
      .replace(/{{jobVerbing}}/g, jobVerbing)
      .replace(/{{mustDos}}/g, mustDos)
      .replace(/{{desire}}/g, desire)
      .replace(/{{job}}/g, job)
      .replace(/{{goal}}/g, goal)
      .replace(/{{tool}}/g, tool);
    
    document.getElementById('outputText').innerHTML = updatedLyrics;
  }
</script>