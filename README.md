# Lab_2_senales_problema_del_coctel

### Configuración del sistema.

![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/1.JPG)

La grabación de audio se llevó a cabo en una sala insonorizada en la Universidad Militar, la cuál fue compartida con otros estudiantes para sus propias tomas, este fue un espacio ideal para capturar las voces de las tres personas hablando simultáneamente con diferentes frases para las tomas. El diagrama de la sala muestra la disposición de los elementos, donde la parte superior del diagrama representa la pared trasera y la parte inferior corresponde a la zona frontal, que cuenta con una ventana y una puerta.
En el diagrama, los cuadrados negros indican la ubicación de las sillas, que fueron colocadas en formación triangular con una separación de aproximadamente 1.5 metros entre ellas y cada silla viendo hacia el centro de la figura que formaron. Cada participante se situó en el centro de dos sillas, con una a su izquierda y otra a su derecha, orientándose hacia el centro del triángulo igualmente. Esta disposición permitió que cada individuo pudiera ver a los otros dos participantes durante la grabación.
Los teléfonos se colocaron en el centro de cada silla con su pantalla en dirección al techo, con el micrófono orientado hacia el centro del triángulo. Tres asistentes adicionales, que no participaron en la grabación, se encargaron de iniciar la grabación simultáneamente en los tres dispositivos. Posteriormente, se utilizó la aplicación "RecForge II" para capturar los audios, ajustando la configuración de los celulares a una frecuencia de muestreo de 44 kHz, en formato mono y con una tasa de bits de 128 kbps. Después de la grabación, se realizó una edición temporal de los archivos de audio para sincronizarlos lo mejor posible.

### Explicación del código.

Para poner los audios que quieras procesar sin que el código se tenga que modificar a gran medida, solo debes subir al colab por medio de archivos tu audio, y reemplazar el nombre que tenga tu audio en _"audio_file = 'nombre de tu audio' "_, y así empezar a correr el programa.

En el código se ilustraron dos gráficas que aportan puntos de análisis interesantes, ya que la primera nos muestra el audio de comparación con el tiempo dada la magnitud que captó en ese momento con las voces de las tres personas que hablaron al mismo tiempo, y la segunda gráfica muestra la incidencia de frecuencias y su intensidad, lo cuál se obtuvo por medio de  la Transformada Rápida de Fourier (FFT), ya que ayuda a pasar la primera gráfica que está en el dominio del tiempo al de la frecuencia, se puede ver en una escala de menor a mayor las magnitudes de estas.

Algo que se puede deducir de esta última gráfica, es que las voces presentan una mayor magnitud entre los 200 hz y 1000 hz, por lo que este puede ser el rango más adecuado para filtrar la señal de otros ruidos y buscar la voz que pueda distinguirse más fácil entre las demás. El resto de las frecuencias pueden llegar a considerar como un ruido ambiente para la señal o un ruido ocasionado por la mezcla final de las frases de las voces, el cuál puede ser reducido.

![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/2.JPG)

Los datos de la segunda gráfica se pueden comparar con el histograma de frecuencias.

![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/3.JPG)

Como primera parte colocamos las librerías a utilizar.

- *_librosa:_* nos permite procesar los datos de los archivos de audio
- *_numpy:_* hacer operaciones matemáticas
- *_butter:_* operación de filtro butterworth
- *_Audio y Display:_* colocar un reproductor de audio, y poder reproducir el sonido

Se leen los archivos para obtener la amplitud y la frecuencia de muestreo para procesar la información.


![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/4.JPG)

Aquí tenemos dos formas de hacer el filtrado de la señal, a través de ayuda de librerías y con transformada de fourier a secas.

en este método es donde más parámetros se pueden configurar, la frecuencia de nyquist, que se define como la mitad de la frecuencia de muestreo, el orden del filtro, los parámetros de frecuencias del filtro, y ya estaría para realizar el filtrado.


![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/5.JPG)

Este método es un poco más matemático pero más sencillo, por lo que solo necesitas la amplitud de sonido, su frecuencia de muestreo, y las frecuencias de corte baja y alta.

![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/6.JPG)

Aunque ambos métodos llegan a eliminar frecuencias del espectro, las voces no se llegan a eliminar del todo, por causas de que las voces varían de frecuencia y esto causa de que tenga fugas de frecuencia a los tonos graves o agudos, tanto a hombres como mujeres.

como último realizamos la ecuación de SNR para comprobar la legibilidad del audio grabado con respecto al ruido ambiente captado, dando un data positivo y alto, en caso de ser cercano a cero o negativo se recomienda regrabar los audio o realizar las tomas en un lugar más silencioso, ya que la calidad del audio seria de muy mala calidad.

los Display(Audio() que nos sirvieron para poder generar un ventana la cual reproducir los audios filtrados como los que no.


![](https://github.com/StarNathaly/Lab_2_senales_problema_del_coctel/blob/main/7.JPG)
