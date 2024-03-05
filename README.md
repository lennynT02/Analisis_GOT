# Función Personaje
La función `Personaje`toma un texto como entrada y realiza un análisis de los personajes mencionados en el texto.
```python

def Personaje(text):

```
Primero, se crea un corpus de texto plano con el archivo de texto proporcionado.

```python

corpus = nltk.corpus.PlaintextCorpusReader('.',text+'.txt')

```
Luego, se extraen las oraciones del corpus.

```python

oraciones = corpus.sents()

```
Se inicializa una lista vacía para almacenar los nombres de los personajes.

```python

personajes = []

```
Para cada oración en las oraciones, se realiza lo siguiente:

```python

for oracion in oraciones:

```
Se une la oración en una cadena.

```python

oracion_str = ' '.join(oracion)

```
Se crea un objeto TextBlob con la oración.

```python

wiki = TextBlob(oracion_str)

```
Se itera sobre los pares de palabras en la oración. Si ambas palabras son nombres propios (indicado por 'NNP') y no son ciertas palabras específicas (como 'Lord' o 'Ser'), se añaden a la lista de personajes.

```python

for i in range(len(wiki.tags)-1):
    if (wiki.tags[i][1] == 'NNP' and wiki.tags[i+1][1] == 'NNP' and wiki.tags[i][0] != "’" and wiki.tags[i+1][0] != "’" 
        and wiki.tags[i+1][0] != "”" and wiki.tags[i][0] != "”" and wiki.tags[i+1][0] != "Lord" and wiki.tags[i][0] != "Lord"
        and wiki.tags[i+1][0] != "Ser" and wiki.tags[i][0] != "Ser"):
        personajes.append(wiki.tags[i][0] + ' ' + wiki.tags[i+1][0])

```
Se calcula el total de personajes.

```python

total_personajes=len(personajes)

```
Se calcula la frecuencia de cada personaje.

```python

frecuencia = nltk.FreqDist(personajes)

```
Finalmente, se imprime el nombre de cada personaje y su frecuencia relativa.

```python

for personaje, frecuency in frecuencia.most_common(30):
    print(f"Personaje:{personaje}--->Frecuencia:{((frecuency/total_personajes) * 100):.2f} %")

```
