@media screen and (min-width: 400px) and (max-width: 800px) {
  body {
    background-color: red;
  }
}

Такой медиа-запрос выполнится только если веб-страница открыта на экране, а ширина вьюпорта находится в диапазоне от 400px до 800px.

____________________
Оператор , (буквально «ИЛИ») позволяет указать набор выражений, при выполнении хотябы одного из которых, выполнится медиа-запрос.

Например, необходимо применить стили в промежутке до 600px или после 900px.

@media (max-width: 600px), (min-width: 900px) {
  body {
    background-color: orange;
  }
}
___________________________

При использовании оператора not обязательно должен быть указан тип носителя, потому что по умолчанию для него будет установлено значение all и выражение not all будет читаться буквально как «не все», и медиа-запрос не выполнится никогда.
_____________________

Mobile First разработке это:

Показать самое важное содержание в первую очередь.
Вебсайт должен быть легковесным и оптимизированным, т. к. скорость подключения мобильной сети может быть слабой в зависимости от местонахождения пользователя.
Веб-сайт не должен загружать больше ресурсов, чем требуется пользователю для получения нужной информации.
Дополнительная информация должна грузиться только по требованию пользователя.

______________________
Ретинизация!!!!!!!!!

Процесс подготовки состоит из экспорта изображений в N-раз больше размера оригинала и сохранения их с соответствующими префиксами @2x и @3x. Для оригинала префикс не нужен.

<!-- Экспорт растровой графики
После чего достаточно задать нужный размер тегу <img> в HTML или CSS коде.
Например, чтобы показать фотографию 200x300 CSS-пикселей на экране с плотностью 2, необходимо подготовить её вариант в размере 400x600 растровых пикселей. Для экрана с плотностью 3 это изображение должно быть 600x900 растровых пикселей.
Процесс подготовки состоит из экспорта изображений в N-раз больше размера оригинала и сохранения их с соответствующими префиксами @2x и @3x. Для оригинала префикс не нужен.
После чего достаточно задать нужный размер тегу <img> в HTML или CSS коде.

<img src="icon.png" width="200" height="300" />
<img src="icon@2x.png" width="200" height="300" />
<img src="icon@3x.png" width="200" height="300" /> -->
_______________________

Отзывчивые изображения
/* Свойства нужно применить ко всем изображениям,
   поэтому используется селектор тега. */
img {
  display: block;
  max-width: 100%;
  height: auto;
}
___________________________
<!-- Дескриптор х используется для фиксированного размера холста, для адаптивной вёрстки -->
   <img 
      srcset="./img.jpg 1x, ./img@2x.jpg 2x"
      src="./img.jpg" alt="pc"
      width="320"> <!-- фиксированный размер холста -->      

        
___________________________________________________
<!-- Дескриптор w используется для  не фиксированного размера холста, для отзывчивой вёрстки -->

 <div class="thumb">
      <img
        srcset="./img.jpg 354w, ./img@2x.jpg 708w, ./img@3x.jpg 1062w"
        src="./img.jpg"
        alt="pc"
       sizes="(min-width: 800px) 33vw, (min-width: 500px) 50vw, 100vw"/>     <!--указываем размер холста на котором будет картинка в порядке убывания, т к браузер берет первое подходящее и не проверяет дальше.  -->
    </div>
_____________________________________
<!-- Следующий пример определяет элемент <picture>, который позволит браузерам загрузить photo.webp, при этом предоставляется альтернатива photo.jpg для браузеров которые еще не поддерживают webp. -->

<picture>
  <source srcset="photo.webp 1x, photo@2x.webp 2x" type="image/webp" />
  <source srcset="photo.jpg 1x, photo@2x.jpg 2x" type="image/jpeg" />
  <img
        srcset="./img.jpg 354w, ./img@2x.jpg 708w, ./img@3x.jpg 1062w"
        src="./img.jpg"
        alt="pc"
       sizes="(min-width: 800px) 33vw, (min-width: 500px) 50vw, 100vw"/>
</picture>
_________________________________
 <!-- Кадрирование (art direction) -->

 <!-- Для экранов шире 600px будет загружен photo-wide.jpg -->
<picture>
  <source srcset="photo-wide.jpg 1x, photo-wide@2x.jpg 2x" media="(min-width: 600px)" />
  <img src="photo.jpg" alt="Фотография" />
</picture>
  _________________________________________

<!-- для фоновых изображений -->

В медиа-функции min-device-pixel-ratio указывается просто значение пиксельной плотности экрана как число коэффициент между физическими и CSS-пикселями.

Так же необходимо указать функцию min-resolution с двумя разными значениями:

dpi (dots per inch) - количество физических пикселей на дюйм экрана. На экранах стандартной плотности пикселей в одном дюйме 96 точек;
dppx (dots per pixel) - количество физических пикселей в одном CSS-пикселе, другими словами это плотность пикселей где 1dppx равен 96dpi.


  /* Базовые стили и 1x изображение если известны размеры */
.box {
  width: 480px;
  height: 320px;
  background-image: url('photo.png');
  background-size: 480px 320px;
}

  /* Базовые стили и 1x изображение если не известны размеры */
.box {  
  background-image: url('photo.png');
  background-size: contain (cover);
}

/* Переопределяем путь к 2x изображению
   если плотность экрана как минимум 2 */
@media (min-device-pixel-ratio: 2),
  (min-resolution: 192dpi),
  (min-resolution: 2dppx) {
  .box {
    background-image: url('photo@2x.png');
  }
}

/* Переопределяем путь к 3x изображению
   если плотность экрана как минимум 3 */
@media (min-device-pixel-ratio: 3),
  (min-resolution: 288dpi),
  (min-resolution: 3dppx) {
  .box {
    background-image: url('photo@3x.png');
  }
}

<!-- если фоновое изображение разно для разных устройств то @media (min-width: tablet/desktop) { тут все плотности экранов x1, x2.x3} -->
_____________________________
  <!--гибридная вёрстка - на мобильнике отзывчивая (так как разные экраны мобильных), а потом адаптивная. Тянись как хочешь, но когда вьюпорт от 480 пикселей - то останься шириной 480 пикселей.-->
  @media screen and (min-width: 480px) {
    width: 480px;
  }

  @media screen and (min width: 768px) {
    width: 768px;
  }
  
  @media screen and (min width: 1200px) {
    width: 1200px;
  }
  _________________________________________


  <!-- aria для читалок -->
 nav > logo + (button (aria-expanded="false" <!-- меню закрыто (тоесть не открыто) --> aria-controls="manu-container" <!-- меню связано по id-->)  > svg (aria-label="переключатель мобильного меню) > use-cross use-menu) 
     > div.menu-container (id="menu-container" <!-- меню связано по id-->) 

 .icon-cross { display:none; }

 ____________________________________



 

