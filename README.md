# Métodos utilizados para detecção de faces
## Quatro técnicas diferentes:

-   Haar cascade (using OpenCV)
-   HOG+SVM (Dlib)
-   MMOD/CNN (Dlib)
-   SSD (OpenCV's DNN module)

## Foram utilizadas as bibliotecas:
-  OpenCV (para leitura das imagens) 
-  numpy (para o processamento das matrizes)
-  google.colab.patches (para visualizar as imagens no ambiente google colab)
-  Dlib

### Testes com haar cascade
Durante o uso da técnica haar cascade trabalhei com o arquivo frontalface_default.xml que já foi treinado pelo algoritmo Adaboost.<br>
O teste com haar cascade consiste em transformar as imagens em escala de cinza para facilitar a detecção da face.
Com as posições do array retornadas da função detectMultScale, foi utilizado para delimitar o retangulo que informa a localização exata da face na imagem.
Para corrigir os falsos positivos, foi feito o redimensionamento das imagens de forma manual e também por escala utilizando scaleFactor.

#### scaleFactor
Utilizado para especificar quanto o tamanho da imagem é reduzido a cada "escala" da imagem. É utilizado para criar a pirâmide de escala.
#### minNeighbors
Controla quantos vizinhos cada janela deve ter para que a área da imagem seja considerada uma face. Quando o algoritmo acha que uma face está em uma determinada região, um maior fator de confiança é retornado. Se existem regiões com alta confiança em uma área, o classificador reportará uma detecção positiva. O classificador detectará múltiplas janelas ao redor de uma face, indicando quantos vizinhos (ou retângulos) são necessários para que uma face seja detectada

### Detecção de olhos, sorrisos, pessoas e objetos.
Foi realizado a detecção de olhos, sorrisos, pessoas e objetos utilizado os respectivos arquivos na pasta cascades.

### Testes com HOG+SVM
Esta técnica orientada a gradientes utiliza a somatoria dos gradientes de direção e magnitude para determinar o histograma final do graiente.<br>
![image](https://user-images.githubusercontent.com/59829877/209368167-2d28eef9-418b-40b9-8568-7f6c6b9ebd33.png)<br>
<br>se quiser saber mais leia https://learnopencv.com/histogram-of-oriented-gradients/
Com a biblioteca Dlib serão feitos os processamentos.
com as posições retornadas da função dlib.get_frontal_face_detector em formato de tupla podemos utilizar para determinar o posicionamento das faces.
Como o proprio nome sugere, esta tecnica não permite identificar faces que estejam de lado.

### Testes com MMOD/CNN
Baseado em margin object detection
Muito preciso, porem requer GPU para executar com velocidade tolerável.
Dlib Model:
mmod_human_face_detector.dat
Esta tecnica baseada em CNN é capaz de detectar faces de todos os angulos (não precisa estar na posição frontal).

### Testes com SSD
Single Shot Multbox Detector
Com esta técnica a imagem é enviada para a camada de entrada da rede neural em modo single shot, ou seja, de uma unica vez.
As tecnicas de regressão são aplicadas a fim de gerar os bounding boxes "retangulos"
