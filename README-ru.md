# GTC Pygame Runtime Support

Интегрированная поддержка разработки приложений Pygame

Этот пакет программного обеспечения может использоваться для разработки приложений Pygame, включая, но не ограничиваясь, игры и приложения формы, и должен выполняться в среде Python с версией выше 3.4.0.

При использовании его вы можете импортировать пакет программного обеспечения следующим образом:

```python
import GTC_Pygame_Runtime_Support as PRS
```

Каждый компонент в пакете программного обеспечения имеет почти одинаковую методику использования и атрибуты, обычно `Class()` представляет конструктор, а `item.operate()` означает отображение компонента на_Surface. Далее будет представлен пример с кнопкой обратной связи, чтобы продемонстрировать вышеуказанные особенности:

```python
import pygame
import GTC_Pygame_Runtime_Support as PRS
screen = pygame.display.set_mode((200, 200))
button = PRS.button_support.FeedbackButton([40, 40], [20, 20], '114', 15, screen, bg_color=[0, 145, 220],
                                           border_color=[209, 240, 255], text_color=[255, 255, 255],
                                           change_color=((0, 145, 220), (0, 225, 0)))
running = 1
clock = pygame.time.Clock()
while running:
    screen.fill((255, 255, 255))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = 0
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0])
    pygame.display.flip()
    clock.tick(60)
```

Как можно видеть, почти всю важную информацию передаётся при определении, поэтому при вызове достаточно передать координаты мыши (mouse_pos) и факт нажатия (effectiveness).

PRS предоставляет полное решение для прокрутки страницы, что может значительно сэкономить волосы программистов:

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as PRS

screen = pygame.display.set_mode((500, 500))
bp = PRS.basic_page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__':
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100):
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bp.add_button_trusteeship(PRS.button_support.FeedbackButton([280, 80], (10, 30), '114514', 62, bp.surface,
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

Эта страница может прокручиваться не только с помощью колеса мыши, но и с помощью перетаскивания мышью, и кнопки могут использоваться нормально после использования функции `add_button_trusteeship()`.

Все слой Surface функциональных компонентов открыт для разработчиков, что позволяет разработчикам изменять слой самостоятельно, когда они недовольны исходным художественным эффектом кнопки. Например, в приведенном выше примере, линии рисуются на прокручиваемой странице. Пользователи могут напрямую получить Surface страницы через `bp.surface` и удобно установить его в качестве фона с помощью `bp.set_as_background()`.
