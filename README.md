# GTC Pygame Runtime Support
Интегрированная поддержка разработки приложений для Pygame

Найти английскую версию? [нажмите здесь](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support)

Этот пакет может быть использован для разработки приложений Pygame, включая, но не ограничиваясь играми и приложениями форм, и должен быть запущен в среде Python старше 3.4.0.

Вы можете загрузить этот пакет с помощью pip

``
$ pip install GTC_Pygame_Runtime_Support
```

Чтобы использовать его, вы можете импортировать пакет следующим образом:

`` python
import GTC_Pygame_Runtime_Support as PRS
```

Каждый компонент в пакете имеет практически идентичное использование и свойства, обычно ``Class()`` для конструктора и ``item.operate()`` для отображения компонента на Surface. Вышеуказанные возможности будут продемонстрированы на примере кнопки обратной связи:

``python
import pygame
import GTC_Pygame_Runtime_Support as PRS
screen = pygame.display.set_mode((200, 200))
button = PRS.button.FeedbackButton([40, 40], [20, 20], '114', 15, screen, bg_colour=[0, 145, 220],
                                           border_colour=[209, 240, 255], text_colour=[255, 255, 255],
                                           change_colour=((0, 145, 220), (0, 225, 0))
бег = 1
часы = pygame.time.Clock()
while running.
    screen.fill((255, 255, 255))
    for event in pygame.event.get(): if event.type == pygame.
        if event.type == pygame.QUIT.
            бег = 0
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0])
    pygame.display.flip()
    clock.tick(60)

``
Как видите, почти вся важная информация передается при ее определении, поэтому все, что нужно, - это передать координаты мыши (mouse_pos) и состояние мыши (mouse_press) при ее вызове.

PRS предоставляет полное решение для прокрутки страниц, что может сэкономить волосы программистов:

``python3
import sys
import pygame
import GTC_Pygame_Runtime_Support as PRS

screen = pygame.display.set_mode((500, 500))
bp = PRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == '__main__': __name__ == '__main__': __name__ == '__main__'.
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bp.add_button_trusteeship(PRS.button.FeedbackButton([280, 80], (10, 30), '114514', 62, bp.surface,
                                                                bg_colour=[0, 145, 220],
                                                                border_color=[209, 240, 255], text_colour=(255, 255, 255),
                                                                change_color=((0, 145, 220), (0, 220, 145))))
    while True.
        mw = [False, False]
        for event in pygame.event.get():: if event.type == pygame.event.get()
            if event.type == pygame.QUIT.
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN: if event.button == 4: sys.exit: sys.exit()
                if event.button == 4: mw[1] = True
                    mw[1] = True
                elif event.button == 5: mw[0] = True
                    mw[0] = True
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0], mw, True)
        pygame.display.flip()
        clock.tick(60)
``
Страница позволяет не только прокручивать страницу с помощью колеса прокрутки, но и перетаскивать ее с помощью мыши, а кнопки отлично работают после использования функции `add_button_trusteeship()`.

Слой Surface всех функциональных компонентов открыт для разработчиков, что позволяет им модифицировать слой, если их не устраивает художественное оформление оригинальных кнопок. Например, в приведенном выше примере с рисованием прямой линии на прокручивающейся странице пользователь может получить Surface страницы напрямую через `bp.surface` и установить его в качестве фона по умолчанию удобным способом через `bp.set_as_background()`. чтобы установить его в качестве фона по умолчанию.

Переведено с помощью www.DeepL.com/Translator (бесплатная версия)
