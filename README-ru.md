# GTC Pygame Runtime Support
Integrated Pygame Application Development Support

什么？你要中文版？那你咋点进俄语版来了？[点这](https://github.com/GTC-Byzantine/GTC-Pygame-Runtime-Support/)

Finding an English version? [click here](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support/)

## Установка пакета
Как и большинство пакетов, этот пакет можно загрузить и установить с помощью pip

```plain
pip install GTC_Pygame_Runtime_Support
```

Если pip взорвется, вы можете скопировать исходный код непосредственно с [Github](https://github.com/GTC-Byzantine/GTC-Pygame-Runtime-Support/).

## Пример использования
### Кнопки
PRS предоставляет три типа кнопок, все они находятся в файле ``button.py``, и мы будем использовать ``FeedbackButton`` в качестве примера.

```python
import pygame
import GTC_Pygame_Runtime_Support as gPRS
screen = pygame.display.set_mode((200, 200))
button = gPRS.button.FeedbackButton([40, 40], [20, 20], '114', 15, screen, bg_color=[0, 145, 220], 
                                    border_color=[209, 240, 255], text_color=[255, 255, 255],
                                    change_color=((0, 145, 220), (0, 225, 0)))
running = 1
clock = pygame.time.Clock()
while running:
    screen.fill((255, 255, 255))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = 0
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3))
    if button.on_click:
        print("clicked")
    pygame.display.flip()
    clock.tick(60)
```

Выполнив приведенный выше код, вы сможете создать кнопку, которая отображает текст 114, а при нажатии на нее в консоль выводится «clicked», причем кнопка будет иметь различную обратную связь в зависимости от действий пользователя.

### Страницы
Типы страниц, предоставляемые PRS, находятся в файле `page.py` и показаны здесь как `PlainPage`.

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__':
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()

    mw = [False, False]
    while True:
        mw = [False, False]
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                if event.button == 4:
                    mw[1] = True
                elif event.button == 5:
                    mw[0] = True
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3), mw, True)
        pygame.display.flip()
        clock.tick(60)
```

Выполнив приведенный выше код, вы сможете создать страницу, которую можно прокручивать колесиком мыши и перетаскивать левой кнопкой, а также самостоятельно менять ее фон, если перед основным циклом вызвать функцию `bp.set_as_background()`.

### Вложенные операции в PRS
В PRS все компоненты отображения могут быть вложены друг в друга с помощью операндов.

#### Вложенные кнопки на страницах
Все компоненты в PRS размещают кнопки одинаковым образом, как показано ниже:

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__':
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bt = gPRS.button.FeedbackButton([40, 40], [20, 20], '114', 10, bp.surface)
    bp.add_button_trusteeship(bt)

    mw = [False, False]
    while True:
        mw = [False, False]
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                if event.button == 4:
                    mw[1] = True
                elif event.button == 5:
                    mw[0] = True
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3), mw, True)
        if bt.on_click:
            print('clicked')
        pygame.display.flip()
        clock.tick(60)
```

PRS обычно добавляет вложенные кнопки в виде `item.add_button_trusteeship(button)`, при этом целевая поверхность объявления кнопки должна указывать на поверхность вложенного объекта, обычно `item.surface`.

#### Вложенные страницы внутри страниц
Принцип в основном тот же, что и выше.

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__':
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    inner_p = gPRS.page.PlainPage([100, 100], [100, 300], [50, 200], bp.surface, wheel_support=True)
    inner_p.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(inner_p.surface, [0, 0, 255], [0, 9 * i], [300, 9 * i])
    inner_p.set_as_background()
    bp.add_page_trusteeship(inner_p)

    mw = [False, False]
    while True:
        mw = [False, False]
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN:
                if event.button == 4:
                    mw[1] = True
                elif event.button == 5:
                    mw[0] = True
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3), mw, True)
        pygame.display.flip()
        clock.tick(60)
```

Из приведенного выше введения вы должны иметь общее представление об особенностях использования PRS.
The Surface layer of all functional components is open to developers, which allows them to modify the layer if they are not satisfied with the artwork of the original buttons. For example, in the above example of drawing a straight line to a scrolling page, the user can get the Surface of the page directly through `bp.surface` and set it to be the default background conveniently through `bp.set_as_background()`. to set it as the default background.
