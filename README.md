##Вольный перевод спецификации — Navigation Timing

###Общее.

Данная спецификация определяет интерфейс для веб приложения, который позволяет узнать затраченное время на доставку документа и его элементов.

###1 Введение

*Эта секция не является нормативом.*

Время ожидания пользователем является важным показателем производительности для Веб приложения. Сценарии на основе механизмов, подобных [[JSMEASURE]](http://www.w3.org/TR/navigation-timing/#JSMeasure), могут обеспечить всеобъемлющий инструментарий для измерения времени ожидания в пределах приложения, во многих случаях, но они не способны предоставить готовый end-to-end период ожидания картинки.

Пример — скрипт снизу, наивно пытается измерить время, затраченное на полную загрузку страницы.
```
<html>
<head>
<script type="text/javascript">

var start = new Date().getTime();
function onLoad() {
  var now = new Date().getTime();
  var latency = now - start;
  alert("page loading time: " + latency);
}

</script>
</head>
<body onload="onLoad()">
<!- Main page body goes from here. -->
</body>
</html>
```
На самом деле скрипт считает время,  после загрузки  и начала выполнения JavaScript. Но это не дает никакой информации о загрузке страницы с сервера.

Для того чтобы узнать точное время, можно использовать интерфейс под названием [PerformanceTiming](http://www.w3.org/TR/navigation-timing/#performancetiming). Этот интерфейс позволяет узнать точное время ожидания пользователем.

Пример сверху можно изменить так, что он будет показывать время от начала запроса до загрузки страницы.
```
<html>
<head>
<script type="text/javascript">
function onLoad() {
  var now = new Date().getTime();
  var page_load_time = now - performance.timing.navigationStart;
  alert("User-perceived page loading time: " + page_load_time);
}

</script>
</head>
<body onload="onLoad()">
<!- Main page body goes from here. -->
</body>
</html>
``` 
