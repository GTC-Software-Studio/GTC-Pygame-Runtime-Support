# GTC Pygame Runtime Support
Поддержка разработки приложений на Pygame

Finding an English version? [click here](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support)

Этот пакет может быть использован для разработки приложений на Pygame, включая, но не ограничиваясь, играми и оконными приложениями. Рекомендуется использовать в среде Python версии выше 3.4.0.

Вы можете установить этот пакет с помощью pip:

```
$ pip install GTC_Pygame_Runtime_Support
```

При использовании вы можете импортировать пакет следующим образом:

```python
import GTC_Pygame_Runtime_Support as gPRS
```

Каждый компонент пакета имеет практически одинаковые методы и свойства использования, обычно `Class()` обозначает конструктор, а `item.operate()` обозначает наложение компонента на Surface. Далее будет показан пример с кнопкой обратной связи, демонстрирующий эти особенности:

```python
import pygame
import GTC_Pygame_Runtime_Support as PRS
screen = pygame.display.set_mode((200, 200))
button = PRS.button.FeedbackButton([40, 40], [20, 20], '114', 15, screen, bg_color=[0, 145, 220],
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
    pygame.display.flip()
    clock.tick(60)

```
Как видно, почти вся важная информация передается при определении, поэтому при вызове достаточно передать координаты мыши (mouse_pos) и состояние мыши (mouse_press).

PRS предоставляет достаточно полное решение для прокрутки страниц, что может значительно сэкономить волосы программистов:

```python3
import sys
import pygame
import GTC_Pygame_Runtime_Support as PRS

screen = pygame.display.set_mode((500, 500))
bp = PRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__':
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bp.add_button_trusteeship(PRS.button.FeedbackButton([280, 80], (10, 30), '114514', 62, bp.surface,
                                                                bg_color=[0, 145, 220],
                                                                border_color=[209, 240, 255], text_color=(255, 255, 255),
                                                                change_color=((0, 145, 220), (0, 220, 145))))
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
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0], mw, True)
        pygame.display.flip()
        clock.tick(60)
```

Эта страница не только позволяет прокручивать страницу с помощью колеса мыши, но также позволяет перетаскивать страницу с помощью мыши. После использования функции `add_button_trusteeship()` кнопки также могут нормально использоваться.

Все Surface слои функциональных компонентов открыты для разработчиков, что позволяет разработчикам изменять слои самостоятельно, если их не устраивает оригинальный художественный эффект кнопки. Например, в приведенном выше примере с рисованием линий на прокручиваемой странице, пользователь может напрямую получить Surface страницы через bp.surface и удобно установить его как фон по умолчанию с помощью `bp.set_as_background()`.
