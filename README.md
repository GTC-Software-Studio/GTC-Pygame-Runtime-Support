# GTC Pygame Runtime Support
Integrated Pygame Application Development Support

Finding an English version? [click here](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support)

нашли русскую версию? [кликните сюда](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support/blob/main/README-ru.md)

This package can be used for Pygame application development, including but not limited to games and forms applications, and should be run on a Python environment older than 3.4.0.

You can download this package using pip

``
$ pip install GTC_Pygame_Runtime_Support
```

To use it, you can import the package like this:

``` python
import GTC_Pygame_Runtime_Support as PRS
```

Each component within the package has almost identical usage and properties, typically ``Class()`` for the constructor and ``item.operate()`` for mapping the component to the Surface. the above features will be demonstrated next using a feedback button as an example:

``python
import pygame
import GTC_Pygame_Runtime_Support as PRS
screen = pygame.display.set_mode((200, 200))
button = PRS.button.FeedbackButton([40, 40], [20, 20], ‘114’, 15, screen, bg_colour=[0, 145, 220],
                                           border_colour=[209, 240, 255], text_colour=[255, 255, 255],
                                           change_colour=((0, 145, 220), (0, 225, 0)))
running = 1
clock = pygame.time.Clock()
while running.
    screen.fill((255, 255, 255))
    for event in pygame.event.get(): if event.type == pygame.
        if event.type == pygame.QUIT.
            running = 0
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0])
    pygame.display.flip()
    clock.tick(60)

``
As you can see, almost all of the important information is passed in when it is defined, so all that is needed is to pass in the mouse coordinates (mouse_pos) and the mouse state (mouse_press) when it is called.

PRS provides a complete solution for scrolling pages, which can save programmers' hair:

```python3
import sys
import pygame
import GTC_Pygame_Runtime_Support as PRS

screen = pygame.display.set_mode((500, 500))
bp = PRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == ‘__main__’: __name__ == ‘__main__’: __name__ == ‘__main__’.
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bp.add_button_trusteeship(PRS.button.FeedbackButton([280, 80], (10, 30), ‘114514’, 62, bp.surface,
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
The page not only allows you to scroll the page using the scroll wheel, but also to drag the page using the mouse, and the buttons work fine after using the `add_button_trusteeship()` function.

The Surface layer of all functional components is open to developers, which allows them to modify the layer if they are not satisfied with the artwork of the original buttons. For example, in the above example of drawing a straight line to a scrolling page, the user can get the Surface of the page directly through `bp.surface` and set it to be the default background conveniently through `bp.set_as_background()`. to set it as the default background.

Translated with www.DeepL.com/Translator (free version)
