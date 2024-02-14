from asciimatics.effects import Stars, Print
from asciimatics.particles import RingFirework, SerpentFirework, StarFirework
from asciimatics.renderers import FigletText, Rainbow
from asciimatics.scene import Scene
from asciimatics.screen import Screen
from random import randint, choice
import sys


def fire(screen):
    scenes = []
    effects = [
        Stars(screen, screen.width),
    ]
    for _ in range(75):
        fireworks = [
            (StarFirework, 25, 30),
            (StarFirework, 25, 30),
            (StarFirework, 25, 35),
            (StarFirework, 25, 35),
            (StarFirework, 25, 35),
            (RingFirework, 20, 30),
            (SerpentFirework, 30, 35),
            (StarFirework, 25, 35),
            (StarFirework, 25, 35),
            (StarFirework, 25, 35),
        ]
        firework, start, stop = choice(fireworks)
        effects.insert(
            1,
            firework(screen,
                     randint(0, screen.width),
                     randint(screen.height // 8, screen.height * 3 // 4),
                     randint(start, stop),
                     start_frame=randint(0, 250)))

    effects.append(Print(screen,
                         Rainbow(screen,FigletText("CS", font = 'isometric3')),
                         screen.height // 2 - 8,
                         speed=1,
                         start_frame=10))
    effects.append(Print(screen,
                         Rainbow(screen, FigletText("is fun!", font = 'bloody')),
                         screen.height // 2 + 4,
                         speed=1,
                         start_frame=20))
    scenes.append(Scene(effects, -1))

    screen.play(scenes, stop_on_resize=True)

Screen.wrapper(fire) 
