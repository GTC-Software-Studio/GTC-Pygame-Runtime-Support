# GTC Pygame Runtime Support
Integrated Pygame Application Development Support

This software package can be used for Pygame application development, including but not limited to games and form applications, and should be run in a Python environment with a version greater than 3.4.0.

When using it, you can import the software package like this:

```python
import GTC_Pygame_Runtime_Support as PRS
```

Each component in the software package has almost the same method of use and attributes, usually `Class()` represents the constructor, and `item.operate()` means to map the component to the Surface. The following will take a feedback button as an example to show the above features:

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
    button.operate(pygame.mouse.get_pos(), pygame.mouse.get_pressed(3)[0])
    pygame.display.flip()
    clock.tick(60)
```

It can be seen that almost all important information is passed in when defined, so only the mouse coordinates (mouse_pos) and whether it is clicked (effectiveness) need to be passed in when calling.

PRS provides a comprehensive scrolling page solution, which can greatly save programmers' hair:

```python
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

This page can not only scroll with the scroll wheel but also drag the page with the mouse, and buttons can be used normally after using the `add_button_trusteeship()` function.

All functional component Surface layers are open to developers, which allows developers to modify the layer themselves when they are not satisfied with the original button's artistic effect. For example, in the above example, lines are drawn on the scrolling page. Users can directly obtain the page's Surface through `bp.surface` and conveniently set it as the default background through `bp.set_as_background()`.
