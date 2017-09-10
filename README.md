# telecommunicatikz
A bunch of macros for drawing schemes with telecommunications devices according to ESKD GOST 2.737-68 in TikZ

Набор макросов для латеховского TikZ чтобы рисовать в нём электрические схемы с устройствами связи, по ЕСКД ГОСТ 2.737-68 (ну или хотя бы чтобы было похоже на ГОСТ)

## Usage (en)
  The devices are created as rectangular nodes with decorations. That means, they have names to refer, and anchors
  inherited from the Rectangular node (namely, north, south..., north east, south west..., and angle anchors like 10, 25, 30, 180...)
  
  Devices are first created, like
  ```
  \Device[Sample]{(2, 0)}{sample};
  \GeneratorSin{(0, 0)}{gen} % The semicolon can be omitted here.
  \Amplifier[log]{(4, 0)}{logamp}
  ```
  and then connected with lines (`\Line` is by definition just a `\draw[very thick, #1]`):
  ```
  \Line (gen.east) -- (sample.west); % A semicolon is mandatory here!
  \Line (sample.east) -- (logamp.west);
  \Line[-latex] (logamp.east) to +(1cm, 0) node[right] {To ADC};
  ```
  Anchors can often be omitted:
  ```
  \Line (gen) -- (sample) -- (logamp) to +(1cm, 0) node[right] {To ADC};
  ```
  
  Devices can also be decorated, for example, with `\MakeRegulated`:
  ```
  \MakeRegulated[$f$]{gen} % A generator with controlled frequency.
  ```
  
  All device creation macros accept two mandatory arguments:
  - device center coordinates in the TikZ form (in parentheses);
  - device node name (is used later to connect devices).
  
  Some device creation macros also accept an optional argument:
  - \Device can be a box with text, which is passed through the optional argument;
  - \amplifier can be provided with a transfer function, e.g. **log**.
  - \MakeRegulated can be provided with a parameter, which is regulated, e.g. frequency.
  
## Usage (ru)
  Обозначения устройств по своему внутреннему устройству представляют собой прямоугольные ноды с добавленными поверх
  декорациями. Таким образом, у них есть имена и якори, взятые от прямоугольных нодов: north, south..., north east, south west..., и якори-углы: 10, 25, 30, 180...
  
  Сначала устройства создаются:
  ```
  \Device[Sample]{(2, 0)}{sample};
  \GeneratorSin{(0, 0)}{gen} % Точку с запятой здесь можно не ставить.
  \Amplifier[log]{(4, 0)}{logamp}
  ```
  а затем соединяются линиями (`\Line` - это `\draw[very thick, #1]`, ни больше ни меньше):
  ```
  \Line (gen.east) -- (sample.west); % Точка с запятой здесь необходима!
  \Line (sample.east) -- (logamp.west);
  \Line[-latex] (logamp.east) to +(1cm, 0) node[right] {To ADC};
  ```
  Якори часто можно не указывать:
  ```
  \Line (gen) -- (sample) -- (logamp) to +(1cm, 0) node[right] {To ADC};
  ```
  
  Также устройства можно декорировать, например, при помощи `\MakeRegulated`:
  ```
  \MakeRegulated[$f$]{gen} % Генератор с регулируемой частотой.
  ```
  
  Все макросы создания устройств принимают на вход два обязательных аргумента:
  - координаты центра в нотации TikZ (в круглых скобках);
  - имя создаваемого нода (далее используется чтобы соединять устройства).
  
  Некоторые макросы создания устройств принимают также дополнительный аргумент:
  - \Device может быть просто "коробкой" с надписью - эту надпись можно передать в дополнительном аргументе;
  - в \amplifier можно указать амплитудную характеристику, например **log**.
  - в \MakeRegulated можно указать регулируемый параметр, например, частоту.
## Макросы/Macros
* `\Device` - абстрактное устройство, прямоугольник с текстом, или пустой. Дополнительный аргумент: текст.
* `\Generator` - генератор ~~с большой буквы~~ с большой буквой G, заполняющей квадрат.
* `\generator` - генератор с маленькой буквой G в верхней половине квадрата. Основа для генераторов с указанной формой сигнала.
* `\GeneratorSquare` - генератор прямоугольных импульсов.
* `\GeneratorSin` - генератор синусоидального сигнала.
* `\GeneratorAF` - генератор синусоидального сигнала звуковой частоты.
* `\Splitter` - делитель мощности с двумя выходами. Выходы рекомендуется подключать к якорям 30 и -30, вход - к west.
* `\Amplifier` - усилитель с большим треугольником.
* `\amplifier` - усилитель с маленьким треугольником в правой нижней части. Дополнительный аргумент: амплитудная характеристика.
* `\Filter` - фильтр.
* `\LowPassFilter` - фильтр нижних частот.
* `\HighPassFilter` - фильтр высоких частот.
* `\BandPassFilter` - полосовой фильтр.
* `\BandStopFilter` - режекторный фильтр.
* `\Modulator` - модулятор. Согласно ГОСТ, сигнал несущей частоты нужно подключать к якорю south, а модулирующий и выходной сигналы - к west и east.
* `\Demodulator` - демодулятор.
* `\Attenuator` - аттенюатор с большим значком "дБ".
* `\Converter` - абстрактный преобразователь. Основа для всех преобразователей с конкретной функцией.
* `\Rectifier` - выпрямитель. Вход переменного тока подклчается к west, выход постоянного - к east.
* `\Inverter` - инвертор. Вход постоянного тока подклчается к west, выход переменного - к east.
* `\DCDCConverter` - преобразователь постоянного тока.
* `\FrequencyConverter` - преобразователь частоты.
* `\FrequencyMultiplier` - умножитель частоты.
* `\FrequencyDivider` - делитель частоты.



## От автора: почему не CircuiTikZ?
Я не стал пытаться прикручивать их к небезызвестному CircuiTikZ, потому что там элементы - это shape, и описываются они не на TikZ (для казуалов вроде меня), а на хардкорном PGF. Я решил, что совершенно не желаю его учить, да и принцип KISS никто не отменял, поэтому сделал не новые шейпы, а просто макросы. Из этого следует:

- для пользователя это не выглядит как ТруЪ TikZ;

+ зато, в отличие CircuiTikZ, свой элемент добавить очень просто.
