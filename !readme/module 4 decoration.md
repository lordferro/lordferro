background-repeat: repeat | repeat-x | repeat-y | no-repeat

repeat - повторять по X и Y. Значение по умолчанию.
repeat-x - повторять только по X, то есть по горизонтали.
repeat-y - повторять только по Y, то есть по вертикали.
no-repeat - не повторять.

<!-- Чаще всего необходимо заполнять высоту. Для этого используется свойство background-size со значением cover. -->
<!-- Иногда фоновое изображение должно заполнять всю ширину элемента. Для этого используется свойство background-size со значением contain. -->

<!-- background-clip. У этого свойства значение по умолчанию border-box. -->

Остальные значения (значения указывают с чего должно начинаться отображение):

!!!!!!!!!!!! background-origin для этого тоже
border-box
padding-box для отображения под всем элементом, кроме border;
content-box для отображения под всем элементом, кроме border и padding;
text для отображения только под текстом. Цвет текста должен быть transparent чтобы фоновое изображение было видно в качестве цвета текста. (Значение `text` может не работать в браузерах на основе `chromium`, поэтому следует дополнительно использовать правило с вендорным префиксом `-webkit-background-clip: text` перед записью `background-clip: text`.)
<!--  -->

background-attachment: scroll| fixed | inherit

scroll - фон прокручиватеся вместе с содержимым. Это значение по умолчанию.
fixed - фон не прокручивается, зафиксирован на месте.

__________________________


________________________
object-fit: fill | contain | cover | scale-down | none

fill - изображение масштабируется без сохранения пропорций, чтобы полностью заполнить контейнер. Значение по умолчанию.
contain - изображение масштабируется с сохранением пропорций, чтобы максимально заполнить контейнер (максимально заполнить ширину).
cover - изображение масштабируется с сохранением пропорций, чтобы полностью заполнить контейнер (максимально заполнить высоту).
scale-down - будет выбрано значение none или contain, чтобы изображение было наименьшего размера.
none - сохраняются исходные размеры изображения, заданная высота и ширина не имеют эффекта.

________________________
object-position: position | initial | inherit

Значением свойства могут быть зарезервированные слова, абсолютные или относительные единиицы измерения. По умолчанию значение 50% 50%, то есть вертикально и горизонтально по центру.

_______________________________
Элемент должен быть display: flex or inline-flex

Создаём место - что перед и после списка будет что то:
.list-link::before,
.list-link::after {
  content: "";
  display: block;
  width: 24px;
  height: 24px;
  background-size: contain;

  /* добавляем иконку огня перед ссылкой */
.list-link::before {
  display: none;
  margin-right: 16px;
  background-image: url("https://cdn-icons-png.flaticon.com/512/599/599502.png");
}

/* показывает иконку при ховере */
.list-link:hover::after {
  display: block;
}

____________________
<!-- градиент начинается с противоположного угла, буквально в верхний левый. -->
background-image: linear-gradient(to top left, red, green);
направление можно задать в градусах 90deg.
background-image: linear-gradient(90deg, red, green);

<!-- Color-stop: -->
background-image: linear-gradient(
  to right,
  #f44336 15%,
  #09792b 40%,
  #00b9ff 65%,
  #ffb800
);
В таком градиенте:

красный цвет (#f44336) будет распространяться от 0% до 15%
зелёный цвет (#09792b) будет распространяться от 15% до 40%
синий цвет (#00b9ff) будет распространяться от 40% до 65%
жёлтый цвет (#ffb800) будет распространяться от 65% до 100%

!!Если колорстопы заданы в пикселях и общая сумма меньше, чем ширина или высота элемента, то получится повторяющийся градиент.

<!--  повтор линейного градиента -->
background: repeating-linear-gradient(
      orange 1px, transparent 2px, transparent 20px);
     ;

<!-- Градиент это плавный переход между цветами, но если двум соседним из них задать одинаковые колорстопы, получим сплошные цвета и резкий переход между ними. Это можно использовать для создания «полосатого» фона. Тоесть каждому цвету задается в процентах сколько он будет занимать (от 15 до 40%) -->

background-image: linear-gradient(
  to right,
  #c64f4f 15%,
  #09792b 15%,
  #09792b 40%,
  #00b9ff 40%,
  #00b9ff 65%,
  #ffb800 65%
);
_______________________________
<!-- Радиальный градиент -->
circle, ellipse at top, bottom, right, left, top right...

 background-image: radial-gradient(
    at center,
    var(--start-color) 10%,
    var(--end-color) 50%

<!-- такаже с колор стопами -->

<!-- повторяющийся градиент -->
background-image: repeating-linear-gradient(
  to left,
  blue,
  blue 20px,
  red 20px,
  red 40px /* Опеределяет размер градиента */
);
_____________________________________
box-shadow: <x-offset> <y-offset> <blur> <spread> <color>

x-offset - горизонтальное смещение. Положительное значение смещает тень вправо от блока, отрицательное – влево. Обязательное значение.
y-offset - вертикальное смещение. Положительное значение смещает тень вниз, отрицательное - вверх. Обязательное значение.
blur - радиус размытия. Чем больше значение, тем сильнее размыта тень. Необязательное значение.
spread - радиус распространения. Положительное значение увеличивает тень, отрицательное - уменьшает. Необязательное значение.
color - цвет тени. Можно использовать любой формат записи цвета. Необязательное значение.

<!-- Внутренняя тень -->
box-shadow: inset <x-offset> <y-offset> <blur> <spread> <color>