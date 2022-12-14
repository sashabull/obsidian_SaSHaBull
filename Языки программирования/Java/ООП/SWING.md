## Компоненты и контейнеры.
В графическом интерфейсе Swing ```должен иметься хотя бы  
оди н контейнер```. А так как контейнеры одновременно являются компонентам и ,  
то один контейнер может содержать в себе другой. Это дает возможность сформировать так называемую ```иерархию включения```, на вершине которой находится  
```контейнер верхнего уровня```.

## Компоненты.
Все компоненты Swing представляются классами , находящимися в пакете 
[[javax.swing]].
**(+) пять наиболее часто используемых компонентов** :  
 - [[JLabel]] , 
 - [[JButton]], 
 - [[JTextField]], 
 - [[JCheckBox]] и 
 - [[JList]]. 
Разобравшись в том, как  они работают, вам будет легче освоить другие компоненты.

## Контейнеры
В Swing определены **два типа** контейнеров. 
1. К **первому типу** относятся следующие **контейнеры верхнего уровня**: 
- [[JFrame]] , 
- JApplet  ```( Контейнер JApplet , который поддерживает аплеты Swing, не рекомендуется  к применению в JDK 9.) ```, 
- [[JWindow]] и 
- [[JDialog]].  

Эти контейнеры ```не наследуют класс JComponent``` , но  они наследуют классы Component и Container библиотеки ```АWГ```. В отличие от  других, легковесных компонентов Swing, **контейнеры верхнего уровня** ```являются  тяжеловесными```. И менно поэтому они образуют отдельную группу в библиотеке  Swing.

```не могут содержаться в других контейнерах```.  
Более того, любая иерархия ```должна начинаться именно с контейнера верхнего уровня```. **(+)** В прикладных программах чаще всего используется контейнер типа **JFrame**.

2. Контейнеры **второго типа** являются легковесными и наследуются от класса  ```JComponent``` .

## **Панели** контейнеров верхнего уровня
В каждом контейнере верхнего уровня определен набор панелей. На **вершине  
иерархии** находится **корневая панель** - экземпляр класса JRootPane.
**Корневая панель** включает в себя 
- **"стеклянную " панель**, 
- **панель содержимого** и 
- **многослойную  панель**.
**(+) В большинстве случаев** у вас не будет возникать необходимость в ee непосредственном использовании.
**(+)** приложение **в основном** будет взаимодействовать с **панелью содержимого**, в которую добавляются визуальные компоненты. Иными словами, добавляя компонент, например кнопку, в контейнер верхнего уровня , вы на самом  деле добавляете его на панель содержимого.

## Менеджеры компоновки
Прежде чем приступить к написан и ю программ средствами Swing, вам ```необходимо получить хотя бы общее представление о менеджерах компоновки```. Менеджер компоновки управляет размещением компонентов в контейнере. В Java определено несколько таких менеджеров. Большинство из них входит в состав [[АWГ]] (т.е. в пакет java.awt), но Swing предоставляет также ряд дополнительных менеджеров компоновки . 
- Все менеджеры компоновки являются экземплярами классов, реализующих и нтерфейс LayoutManager. 
- ( Некоторые из менеджеров  компоновки реализуют интерфейс LayoutManager2 . ) 
Ниже перечислен ряд менеджеров компоновки, которые доступны для разработчиков, используюших  библиотеку Swing.  

---
- [[FlowLayout]]  - Простой менеджер компоновки, размещающий компоненты слева  
направо и сверху вниз. (Для некоторых региональных настроек  компоненты располагаются справа налево.)  
- [[BorderLayout]]  - Располагает компоненты по центру или по краям контейнера. Этот  
менеджер принят по умолчанию для панели содержимого 
- [[GridLayout]] - Располагает компоненты в ячейках сетки, как в таблице  
- [[GridBagLayout]] - Располагает компоненты разных размеров в ячейках сетки с  
регулируемыми размерами  
- [[BoxLayout]] - Располагает компоненты в вертикальном или горизонтальном  
направлении  
- [[SpringLayout]] - Располагает компоненты с учетом ряда ограничений

---

**(+)** Для панели содержимого менеджером компоновки **по умолчанию** является  
[[BorderLayout]] . Этот менеджер определяет в составе контейнера **пять областей**,  
в которые могут помещаться компоненты . 
- **Первая область** располагается посредине и называется **центральной**. 
- Остальные четыре располагаются в соответстви и со сторонами света и носят такие названия: 
  - **северная**, 
  - **южная**, 
  - **восточная**  и 
  - **западная**. 
**(+) По умолчанию** компонент, добавляемый на панель содержимого,  
располагается в центральной области . Для того чтобы расположить компонент в  
другой области , следует указать ее имя.

**(+)** Несмотря на то что ```возможностей, предоставляемых менеджером компоновки BorderLayout, зачастую оказывается достаточно```, иногда возникает потребность в других менеджерах компоновки.

**(+) К числу самых простых** относится менеджер компоновки ```FlowLayout```, который размещает компоненты построчно:  
- слева направо и 
- сверху вниз. 
Заполнив текущую строку, он переходит к следующей. 
Такая компоновка предоставляет лишь ограниченный контроль над расположением компонентов, хотя и проста в применении. Однако ```при изменении  размеров контейнера расположение компонентов может измениться```.

```java
import javax.swing.*;  
import java.awt.*;  
  
/**  
 * простая Swing программа * по Шилдт Г. Java для начинающих. 7-ое изд. 2019. */public class SwingDemo {  
    /**  
     * конструктор     */    public SwingDemo(){  
        // создание контейнера Верхнего уровня  
        JFrame jfrm = new JFrame("Простое приложение Swing по Шилдт Г.");  
        jfrm.setSize(500, 250);  
        jfrm.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);  
  
        // контейнер вложенный  
        JLabel jlabel1 = new JLabel("Программирование интерфейса с помощью Swing.");  
        jfrm.add(jlabel1, BorderLayout.NORTH);  
  
        jfrm.setVisible(true);  
    }  
}

public class Main {  
    public static void main(String[] args) {  
        // создание фрейма в потоке диспетчеризации событий,  
        // иначе могут быть проблемы при запуске нескольких фреймов.        
        SwingUtilities.invokeLater(new Runnable(){  
            @Override  
            public void run() {  
                new SwingDemo();  
            }  
        });  
    }  
}
```

Объект типа SwingDemo создается _здесь не в основном потоке приложения_,  
а в потоке **диспетчеризации событий**, и вот почему. 
**(!) Обычно** программы Swing  управляются событиям и . Например, когда пользователь активизирует GU I-компонент, генерируется соответствующее событие. Событие передается приложению путем вызова обработчика событий , определяемого приложением.  
```Однако данный обработчик выполняется не в главном потоке приложения, а в потоке диспетчеризации событий``` , предоставляемом библиотекой Swing. Таким  образом, несмотря на то что обработчики событий определяются в программе,  они выполняются в потоке, создаваемом вне программы. Чтобы избежать возможных проблем (например, попытки двух потоков одновременно обновить  один и тот же компонент) , ```все компоненты GUI библиотеки Swing должны создаваться и обновляться в потоке диспетчеризаци и событий , а не в главном потоке приложения```. Однако метод main( ) выполняется в основном потоке и  поэтому ```не может напрямую создавать экземпляры класса SwingDemo``` . Что он может, так это создать объект типа Runnable , выполняющийся в потоке диспетчеризации событий , и поручить создан ие GUI этому объекту.  
Для создания кода GUI в потоке диспетчеризации событий ```необходимо использовать один из двух методов```, определенных в классе SwingUtilities :  
 - **(+)** [[invokeLater()]] - сразу же возвращает управление вызывающему методу. **Как правило**, используется этот метод; 
 - [[invokeAndWait()]]  - ожидает возврата из метода  run ( ) .


## Обработка событий Swing
Механизм обработки событий , используемый в Swing, называется ```моделью  
делегирования событий```.
### Концепция этой модели:
```Источник события``` (нечто на форме или таймер) 
1. _генерирует_ событие и 
2. _отсылает_ его одному или нескольким ```слушателям```.  
При использовании этого подхода ```слушатель```:
1. просто ждет до тех пор, пока не  получит событие. 
2. Как только событие получено, 
3. слушатель обрабатывает и возвращает его. 
**(+) Преимущество этого подхода** заключается в том , что логика приложения, ответственная за обработку событий , четко отделена от логики интерфейса пользователя , которая генерирует события . Таким образом интерфейс  пользователя может **"делегировать" обработку события** отдельной части кода.  
В модели делегирования событий слушатель ```должен регистрировать источник```,  
чтобы иметь возможность получать события .

## События
Суперклассом для всех событий является [[java.util.EventObject]]. 
Многие  события объявлены в пакете [[java.awt.event]]. 
События, которые связаны исключительно со Swing, находятся в пакете [[javax.swing.event]].

## Источники событий
**Источник события** - это объект, генерирующий событие. 
1. Как только источник генерирует событие, 
2. он тут же отсылает его **всем зарегистрированным** слушателям. 
Поэтому для получения события **слушатель** ```должен зарегистрироваться в источнике этого события```. 
В Swing регистрация слушателей в источнике  события осуществляется путем вызова метода для исходного объекта события.  
Обычно для событий используется следующее соглашение о наименовании:  
```java
puЫic void addTипListener ( TипListener се)
```  
где ```Тип``` - это название события, а ```се``` - ссылка на слушателя события . 

Например, 
- метод, который регистрирует слушателя события клавиатуры, называется ```addKeyListener()``` . 
- Метод, которы й регистрирует перемещение указателя мыши, называется ```addMouseMotionListener()```.

Источник также ```должен поддерживать метод, который позволяет отменять  
регистрацию указанного типа события```. В Swing при этом используется метод,  
для которого применяется следующее соглашение о наименовани и :  
```java
puЫic void removeTипListener ( TипListener се)  

```
И снова ```Тип``` - это название события, а ```се``` - ссылка на слушателя события.  
Например, для удаления слушателя клавиатуры можно воспол ьзоваться методом 
```java 
removeKeyListener();
```

```Методы, которые добавляют или удаляют слушателей, поддерживаются источником```, генерирующим события . 
Например, как будет вскоре показано, класс [[JButton]] является источником событий [[ActionEvents]] , свидетельствующих о выполнении какого-либо действия, такого как нажатие кнопки . Таким  образом, класс [[JButton]] _поддерживает методы , применяемые для добавления  или удаления слушателя действия_.

## Слушатели событий
**Слушатель** - это объект, который извещается о произошедшем событии .  
К данному объекту предъявляются **два основных требования**. 
- **Во-первых**, он  ```должен быть зарегистрирован в одном или нескольких источниках``` для получения определенного типа событий . 
- **Во-вторых**, он ```должен реализовать метод для получения и обработки событий``` .

Методы, которые получают и обрабатывают события Swing, определены в наборах интерфейсов, таких как 
- [[java.awt.event]] и 
- [[javax.swing.event]] . 
Например, интерфейс [[ActionListener]] определяет метод, который обрабатывает  событие [[ActionEvent]]. Любой объект может принимать и обрабатывать это событие, если поддерживается реализация интерфейса [[ActionListener]].

А сейчас сформулируем [[очень важный принцип]]: обработчик событий ```должен выполнять свою работу быстро и сразу же завершаться```. В большинстве случаев он ```не должен участвовать в выполнении длительных операций``` , поскольку  это замедлит работу всего приложения. 
**Для выполнения ресурсоемких операций понадобится отдельный поток.**

## Классы событий и интерфейсы слушателей
Классы , которые представляют события, определены в ядре механизма обработки событий Swing. 
В корне иерархии классов событий находится класс  [[EventObject]] , которы й помещен в пакет [[java.util]] . Это суперкласс для всех  событий в Java. 
Класс [[AWTEvent]] , объявленный в пакете [[java.awt]] , является  подклассом [[EventObject]] . Это суперкласс (прямым или косвенным образом )  для всех основанных на [[АWТ]] событиях, используемых моделью делегирования событий .
И хотя Swing использует события [[АWТ]], кроме них добавлены еще собственные события. Как упоминалось ранее, эти события находятся в пакете  [[javax.swing.event]] . Таким образом , Swing поддерживает большое число событий . 

---
Класс события  - Описание  (Соответствующий  слушатель событий)

---
[[ActionEvent]]  - Генерируется при выполнении  действия, которое происходит  в элементе управления, например щелчок на кнопке  ([[ActionListener]])
[[ItemEvent]] - Генерируется при выборе элемента, например после щелчка на флажке ([[ItemListener]])
[[ListSelectionEvent]] - Генерируется при изменении выделения в списке ([[ListSelectionListener]])


---
[[Java]]
[[Шилдт Г. Java. Руководство для начинающих. 7 изд. (JDK 9,10). 2019 (810 стр)]]
[Java docs (oracle)](https://docs.oracle.com/javase/tutorial/uiswing/components/frame.html)
