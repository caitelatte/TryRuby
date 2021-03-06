---
lang:   RU
title:  Благородные родственники
answer: ^The Two Noble Kinsmen$
ok:     Так намного лучше.
error:  
load:   prev
---

Итак, теперь у нас есть список пьес из Интернета. Список был в формате json.
К счастью для нас Ruby любезно предоставляет метод преобразования данных json в hash Ruby.
Метод _get\_shakey_ сделает это за нас.

Но так как структура json-данных сохраняется в hash, ее все-таки трудно читать.
Давайте напишем метод для показа игр.

Если вы внимательно изучите список пьес, вы увидите, что у него есть своего рода вложенный
состав. (Это действительно довольно распространено в данных, которые вы получаете из Интернета.)
Выглядит так:

<ul>
  <li>"William Shakespeare"
  <ul>
      <li>"1"
      <ul>
        <li>"title": "The Two Gentlemen of Verona"</li>
        <li>"finished": 1591</li>
      </ul>
      </li>
      <li>"2"
      <ul>
        <li>"title": "The Taming of the Shrew"</li>
        <li>"finished": 1591</li>
      </ul>
      </li>
      <li>...</li>
  </ul>
  </li>
</ul>

Чтобы перечислить пьесы, нам сначала нужно получить доступ к верхнему элементу словаря «Уильям Шекспир» по его названию.
Затем мы должны __iterate("шагать")__ по каждому элементу за ним.

Ruby имеет метод для итерации. Он называется __each__. Мы видели это раньше, когда
создавая нашу систему рейтинга книг.

Все, что возвращает метод __each__, передается блоку:

    s = get_shakey
    
    s["William Shakespeare"].each { |key, val|
      puts val["title"]
    }
