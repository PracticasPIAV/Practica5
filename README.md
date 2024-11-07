# Práctica 5: Detección de características

**Integrantes:** Alejandro Bolaños García y David García Díaz

## Explicación del código en Python

### Importación de bibliotecas
Las bibliotecas utilizadas incluyen:
- `cv2` (OpenCV) para procesamiento de imágenes,
- `numpy` para manejo de arrays,
- `tkinter` para la interfaz gráfica,
- `Image` de PIL para cargar imágenes,
- `pyplot` de Matplotlib para visualización.

### Variables globales
Se definen varias variables globales para controlar la imagen y las transformaciones:
- `drawing`: Estado del dibujo para la selección de área.
- `ix`, `iy`: Coordenadas iniciales de la selección.
- `fx`, `fy`: Coordenadas finales de la selección.
- `img`: Imagen original.
- `cropped_image`: Imagen recortada seleccionada.
- `transformed_image`: Imagen transformada.
- `w`, `h`: Ancho y alto de la imagen original.

### Función `update_transformation()`
Actualiza todas las transformaciones y ajusta la ventana de visualización. Primero, verifica si la imagen está cargada, luego:
1. Escala la imagen con `cv.resize()`.
2. Crea una matriz de transformación para rotación y traslación con `cv.getRotationMatrix2D()`.
3. Aplica rotación y traslación con `cv.warpAffine()`.
4. Ajusta el tamaño de la ventana de visualización y muestra la imagen transformada usando `cv.namedWindow()`, `cv.resizeWindow()` y `cv.imshow()`.

### Función `draw_figures()`
Callback para el ratón que permite seleccionar una región en la imagen:
1. Al presionar el botón izquierdo, se establecen las coordenadas iniciales de la selección.
2. Al mover el ratón, se dibuja un rectángulo.
3. Al soltar el botón izquierdo, se definen las coordenadas finales y se llama a `crop_image()` para recortar la región seleccionada.

### Función `crop_image()`
Recorta la región seleccionada de la imagen usando las coordenadas iniciales y finales.

### Función `sift_matches()`
Realiza el emparejamiento de características SIFT entre la región seleccionada y la imagen transformada:
1. Verifica si existen ambas imágenes.
2. Convierte las imágenes a escala de grises usando `cv.cvtColor()`.
3. Obtiene valores de SIFT desde los sliders de la interfaz.
4. Detecta y calcula características SIFT en ambas imágenes con `sift.detectAndCompute()`.
5. Realiza emparejamiento con el algoritmo BFMatcher y dibuja los mejores `matches` con `cv.drawMatches()`.
6. Muestra los `matches` en OpenCV y Matplotlib usando `cv.imshow()` y `plt.imshow()`.

### Función `open_file()`
Abre y preprocesa una imagen desde un archivo:
1. Usa `filedialog.askopenfilename()` de Tkinter para seleccionar el archivo.
2. Carga la imagen con `Image.open()` de PIL y la convierte a array de NumPy.
3. Convierte la imagen a escala de grises, mejora el contraste y aplica suavizado.
4. Muestra la imagen en una ventana de OpenCV con `cv.imshow()`.

### Funciones de callback de los sliders
Actualizan las transformaciones cuando se cambian los valores de los sliders en la interfaz gráfica, llamando a `update_transformation()` para aplicar todas las transformaciones.

### Configuración de la interfaz de Tkinter
Crea una ventana de Tkinter y configura los elementos de la interfaz gráfica, como etiquetas, sliders y botones.

## Conclusión
Durante el uso del algoritmo SIFT, observamos que al aplicar grandes escalas a las imágenes, a menudo no se capturaban todas las características de manera precisa. Esto parece estar relacionado tanto con la calidad de las imágenes como con las transformaciones aplicadas, que afectan la precisión del detector. Además, intentamos comparar una región de interés en una imagen con otra imagen distinta para detectar derrames cerebrales, pero el enfoque no resultó exitoso, por lo que descartamos esta parte de la implementación.
