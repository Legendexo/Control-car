rf-car
------
Bu HackRF ilə RC avtomobillərinə nəzarət etmək üçün kiçik bir proqramdır. RC oyuncaqlarının əksəriyyəti eyni protokoldan istifadə edir, buna görə oyuncağın işlədiyi tezliyi tapmaq lazımdır. Mənim vəziyyətimdə 40.684 MHz-dir. RC oyuncağınız 8 istiqamətdə (irəli, geriyə, sola, sağa, irəli-sağa, irəli-sola, geriyə-sağa, geriyə-sola) hərəkət edə bilərsə, bu proqramı idarə etmək üçün istifadə edə biləcəyiniz böyük bir şans var. .

Bunu hərəkətdə görə bilərsiniz:



.. image:: screenshot.png
   :target: https://youtu.be/itS2pWkgNrM

Proqram necə işləyir
Uzaqdan idarəetmə uzun və qısa pulslarla OOK modulyasiyasından istifadə edir. Bir uzun nəbz üç qısa nəbzə bərabərdir. Məsələn, avtomobili irəliyə aparmaq üçün 4 uzun puls göndərmək lazımdır, ardınca 10 qısa pulsasiya. RC-dən siqnal yazmaqla hər istiqamətə nəzarət ardıcıllığını asanlıqla tapa bilərik və sonra inspectrum ilə təhlil edə bilərik :

.. image:: inspectrum.png
   :scale: 67 %

To synthesize the signal with the HackRF, we need to transmit
``SAMPLE_RATE/SYMBOL_RATE`` samples ('1' or '0') for each bit of the control
sequence. We can find the ``SYMBOL_RATE`` with inspectrum, it is about 2018.
We choose the ``SAMPLE_RATE`` to be 2M.

build & run
-----------
The program depends only on SDL2, SDL2_image and libhackrf. To build on Linux::

    $ sudo apt-get install libsdl2-dev libsdl2-image-dev libhackrf-dev
    $ make
    $ ./rf-car

To build on OSX::

    $ brew install sdl2 sdl2_image hackrf
    $ make
    $ ./rf-car

