# GTC Pygame Runtime Support
Integrated Pygame Application Development Support

什么？你要中文版？那你咋点进英文版来了？[点这](https://github.com/GTC-Byzantine/GTC-Pygame-Runtime-Support/)

нашли русскую версию? [кликните сюда](https://github.com/GTC-Software-Studio/GTC-Pygame-Runtime-Support/blob/main/README-ru.md)

## Package Installation
Like most packages, this package can be downloaded and installed using pip

```plain
pip install GTC_Pygame_Runtime_Support
```

If pip explodes, you can copy the source code directly from [Github](https://github.com/GTC-Byzantine/GTC-Pygame-Runtime-Support/).

## Sample usage
### Buttons
PRS provides three types of buttons, all of which are located in the ``button.py`` file, and we'll use the ``FeedbackButton`` as an example.

```python
import pygame
import GTC_Pygame_Runtime_Support as gPRS
screen = pygame.display.set_mode((200, 200))
button = gPRS.button.FeedbackButton([40, 40], [20, 20], ‘114’, 15, screen, bg_colour=[0, 145, 220], border_color=[209, 220], [0, 145, 220], [0, 145, 220], [0, 145, 220]) 
                                    border_colour=[209, 240, 255], text_colour=[255, 255, 255],
                                    change_color=((0, 145, 220), (0, 225, 0))) # Generate button
running = 1
clock = pygame.time.Clock()
while running: # main loop
    screen.fill((255, 255, 255))
    for event in pygame.event.get(): if event.type == pygame.
        if event.type == pygame.QUIT.
            running = 0
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)) # Button mapping at the button.
    if button.on_click.
        print(‘clicked’)
    pygame.display.flip()
    clock.tick(60)
```

Running the above code, you will be able to create a button that displays the text 114, and when you click it, the console will output ‘clicked’, and the button will have different feedback depending on the user's action.

### Pages
The page types provided by PRS are located in `page.py` and are shown here as `PlainPage`.

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == ‘__main__’: __name__ == ‘__main__’: __name__ == ‘__main__’.
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()

    mw = [False, False]
    while True.
        mw = [False, False]
        for event in pygame.event.get(): if event.type == pygame.
            if event.type == pygame.QUIT.
                sys.exit()
            elif event.type == pygame.MOUSEBUTTONDOWN: if event.button == 4: sys.exit: sys.exit()
                if event.button == 4: mw[1] = True
                    mw[1] = True
                elif event.button == 5: mw[0] = True
                    mw[0] = True
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3), mw, True)
        pygame.display.flip()
        clock.tick(60)
```

Running the above code, you will be able to create a page that can be scrolled by the mouse wheel and dragged by the left mouse button, and you can change its background by yourself, as long as you call the function `bp.set_as_background()` before the main loop.

### Nested operations in PRS
In PRS, all display components can be nested by means of trusteeship.

#### Nesting Buttons in Pages
All components in PRS host buttons in the same way, as shown below:

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == ‘__main__’: __name__ == ‘__main__’: __name__ == ‘__main__’.
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    bt = gPRS.button.FeedbackButton([40, 40], [20, 20], ‘114’, 10, bp.surface)
    bp.add_button_trusteeship(bt)

    mw = [False, False]
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
        bp.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3), mw, True)
        if bt.on_click.
            print(‘clicked’)
        pygame.display.flip()
        clock.tick(60)
```

PRS usually adds nested buttons in the form of `item.add_button_trusteeship(button)`, while the target surface of the button declaration should point to the surface of the nested object, usually `item.surface`.

#### Nesting pages within pages
The principle is basically the same as above.

```python
import sys
import pygame
import GTC_Pygame_Runtime_Support as gPRS

screen = pygame.display.set_mode((500, 500))
bp = gPRS.page.PlainPage([300, 300], [300, 1000], [100, 100], screen, 1.4, True)

if __name__ == ‘__main__’: __name__ == ‘__main__’: __name__ == ‘__main__’.
    clock = pygame.time.Clock()
    bp.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(bp.surface, [0, 0, 0], [0, 10 * i], [300, 10 * i])
    bp.set_as_background()
    inner_p = gPRS.page.PlainPage([100, 100], [100, 300], [50, 200], bp.surface, wheel_support=True)
    inner_p.surface.fill((255, 255, 255))
    for i in range(100): pygame.draw.
        pygame.draw.line(inner_p.surface, [0, 0, 255], [0, 9 * i], [300, 9 * i])
    inner_p.set_as_background()
    bp.add_page_trusteeship(inner_p)

    mw = [False, False]
    while True: mw = [False, False]
        mw = [False, False]
        for event in pygame.event.get(): if event.type == pygame.
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
```

With the above introduction, you should be able to have a general understanding of the characteristics of using PRS.
